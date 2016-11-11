---
layout: post
title: Easy way to debug software state in real time
description: "Neat trick to debug software in real time"
modified: 2016-04-26
tags: [Programming, Debugging, RealTimeProgramming]
---
<figure class="center">
  <img src="{{site.url}}/images/rubberDuck.jpeg" alt=""></a>
	<figcaption><a href="https://en.wikipedia.org/wiki/Rubber_duck_debugging" title="Rubber Duck Debugging">https://en.wikipedia.org/wiki/Rubber_duck_debugging</a></figcaption>
</figure>

By no means the approach I’m showing here is revolutionary. The neat little trick immensely helped me once and I thought maybe it will be helpful for someone in the future.
Imagine the situation:

<!-- more -->
>You are working with a long function in a real time system. The system can have different states at the time. The states depend on the real-time behaviour of the system therefore using conventional debugger and breakpoints are not available to you. You also can’t use strings and don’t have any logging capabilities. Imagine that the only thing available to you is one variable that you can view in real time, plus you have access to all variables that determine particular states. How do you debug the states that are present at every iteration?

Sounds complicated? Hopefully the following snippet will make it slightly more clear:

{% highlight python %}
import random
import time

while True:
    randomInt = random.randint(0,100)
    randomNormalized = random.random()
    caseLessThenHalf = (randomNormalized < 0.5)
    caseEven = ((randomInt % 2) == 0)
    caseMoreThanTen = (randomInt > 10)

    if(caseLessThenHalf):
        #your logic
    elif(caseMoreThanTen):
         #your logic
    else:
         #your logic

    if(caseEven and caseMoreThanTen):
         #your logic
    else:
         #your logic
{% endhighlight %}

I tried to make the code simple just to present the idea. Let’s assume that the system allows you to see state_variable after each iteration (save it to file, print it to the console, graph it etc.).

Here is the (possibly) non-revolutionary way to easily show the states in real time:

{% highlight python %}
import random
import time

caseCounter = 0
randomInt = random.randint(0,100)
randomNormalized = random.random()
caseLessThenHalf = (randomNormalized < 0.5)
caseEven = ((randomInt % 2) == 0)
caseMoreThanTen = (randomInt > 10)

if(caseLessThenHalf):
    caseCounter += 1
elif(caseMoreThanTen):
    caseCounter += 2
else:
    caseCounter += 4

if(caseEven and caseMoreThanTen):
    caseCounter += 8
else:
    caseCounter += 16

print (caseCounter)
{% endhighlight %}

### Interpreting the output
The only thing left is to interpret the output. Let’s say our state variable is 10 (2+8), here is what we know:

1. RandomNormalized is >= 0.5 and randomInt is more than ten (caseCounter += 2)

2. Not only is your randomInt more then ten but it’s also even (caseCounter += 10)

You see 17 on the output?

1. Your randomNormalized is < 0.5 (caseCounter += 1)

2. randomInt is either not even or less than ten (caseCounter += 16)

Here, [have a play](https://repl.it/CJBU/0/).

In my particular case where we used this approach we were able to plot the state_variable on the graph after each iteration, because we were using powers of 2 we immediately knew what was the state of the system. Ultimately it allowed us to quickly solve the problem but I would always recommend refactoring instead of having to painfully debug the code.

### How to extend it?
The code I showed you is far away from being neat. If I were to use this approach more than once I would probably do the following (depending on the language/system etc.):

1. Put all the logic in a separate class

2. Have resetCounter function that I call at the beginning of loop/function of interest

3. Have incrementCounter(int, string) function to which you provide number to increment the counter by and string with function name

4. Have getCounter() and printCounter() functions that provide you with the number stored by the counter or print all the functions that were called
