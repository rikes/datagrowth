---
layout: post
title: Don't name your variables 'temp'
description: "Learn why temp is not a good variable name"
modified: 2016-04-16
comments: true
tags: [Programming, CleanCode]
image:
  feature: facepalm.jpeg
---
You know what? Just don’t name your variables temp. It’s an incredibly bad practice (no, I don’t have OCD). I saw many variations of usage of temp variables in all kinds of situations. But maybe I’m just unlucky. Let me show you some examples:

<!-- more -->

## Justified case (pseudo C#)

{% highlight csharp %}
private void swap(ref int lhs, ref int rhs)
{
    int temp = lhs;
    lhs = rhs;
    rhs = temp;
}
{% endhighlight %}

That’s the only type of problem I can think of when naming variable temp is acceptable. Let’s jump to some horror stories.

## The horror (pseudo C)

{% highlight c %}
void fillGlobalVariables()
{
    double temp_double;
    float temp_float = 0f;
    int temp_int;
    char c;
    ...
    while()
    {
        c = serial_read(...); //receive one byte from serial port and put it into c
        switch(c)
        {
            case 0x66: //<s>Don't use const's because they suck</s>
                byte[] received_bytes = serial_read(..,4); //read 4 bytes for int
                temp_int = convert_bytes_to_int(received_bytes);
                break;
            case 0x75:
                //read 8 bytes from serial
                temp_double = convert_bytes_to_double(received_bytes) + 600d / 1.454332d; //apply magic conversion;
                break;
            case 0x43:
                //read 4 bytes from serial
                temp_float = convert_bytes_to_float(received_bytes);
             ...
        }  
        ...
        if (c == 0x6B)
        {
            if(temp_float > 0)
            {
                temp_int += (int)temp_float + 10; //I really hate consts at this point
            }
            else
            {
                temp_int += (int)temp_double;
            }
            my_public_variable = temp_int;
            ...
        }
    }
}
{% endhighlight %}

This should roughly get you an idea what this abomination of a function looked like. It was meant to grab a single flag from the serial port. The flag indicated what data is coming next on the port. Since you know what type of data you are going to receive you should read as many bytes as you need for the given type. Then the code was performing some magic calculations to finally put the correctly formatted value to some struct or global variable.


The function was around 600 lines long. My biggest issue with the code was that the temp variables were used all over the function and they were not simply used as containers for holding the values, they were often modified in different places and assigned to different variables.


Clearly the design above is flawed. Some people might argue that it’s worth to reuse variables this way to save memory. I disagree for two reasons:
1. Readability of the code is way more important than performance. If you are worried about the performance then code it properly first and then try to optimize your code if you run into performance issues.
2. The compiler should be quite good when dealing with scopes. If you declare your variable within an if statement and the condition for this statement is not met then the variable should not be constructed, saving you some space.

### How would I fix the code?
Depending on the amount of time I had I would:

* Do a heavy refactoring, create lots of smaller functions to handle each received item independently
* I would substitute temp variables with lots of meaningful variable names, then having more clear idea what variable is accessed where I would try to limit their scope as much as possible (ideally to the single cases in switch statement).

## Second horror story
{% highlight c %}
void some_function()
{
    float temp_a;
    float temp_b;
    float temp_c;
    //please, kill me
    ...
}
{% endhighlight %}

This code… It’s real and it’s out there somewhere being executed right now. All the temp values were used in some matrix calculations. Simply don’t do that. If you don’t know what’s wrong about this code then go and read **Clean Code**,
if you still don’t know why it’s bad then read **Code Complete**. If you still don’t understand what’s wrong with this approach then mail me, I want to meet you.

## Words of wisdom
Here is what Steve McConnell says on temp variables in Code Complete (chapter 10.8):
>Use each variable for one purpose only. It’s sometimes tempting to use one variable in two different places for two different activities. Usually, the variable is named inappropriately for one of its uses or a “temporary” variable is used in both cases (with the usual unhelpful name x or temp).

## Wrap up
Do your best to give meaningful names to the variables. If you can’t then at least substitute every occurrence of ‘temp’ with unicorn, at least it will be more cute that way.

What happens if you keep giving meaningless names to your variables?
<figure class="center">
  <img src="{{site.url}}/images/taken.jpeg" alt="Guy from taken threatening someone over the phone">
</figure>
