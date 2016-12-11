---
layout: post
title: Git intermediate
description: "Check if you know git on intermediate level"
modified: 2016-12-11
comments: true
tags: [Git, Programming, CleanCode]
image:
  feature: Git-logo.png
  credit: Wikimedia
  creditlink: https://commons.wikimedia.org/wiki/File:Git-logo.svg
---
Are you unsure about the level of your Git skills? Or did you start using Git recently and would like some pointers on where to go next? I hope I will be able to help you in both cases.

# It's going to be subjective

I don't know of any metrics that you can use to assess one's level of any version control system, therefore this article will be heavily subjective. If you know everything I mention in this article then in my personal opinion you can claim you know Git on at least intermediate level. If you aim at higher level of understanding Git then I would suggest you eventually go through [Git source code](https://github.com/git/git) and hopefully contribute to the development.

This article assumes you have at least basic understanding of Git, if you are just starting with Git then please consider [covering the basics first](https://try.github.io/levels/1/challenges/1). It also assumes you are working with Git console (IDEs do not count!). Without further due let's get to the fun parts!
<!-- more -->

## Managing repositories and Git client

- You know how to create and configure repository on a hosting service  ([github](https://github.com/), [gitlab](https://about.gitlab.com/), [bitbucket](https://bitbucket.org/) etc.) of your choice
- You know how to initiate a local repository and link it to the hosting service
- You know what .gitignore is for, you know how to create one and how to exclude individual files, all files with a given extension and whole directories [[1](https://git-scm.com/docs/gitignore)]
- You know how to configure username and e-mail for your Git client [[2](https://git-scm.com/book/en/v2/Getting-Started-First-Time-Git-Setup)]
- You know how to setup ssh identification [[3](https://docs.gitlab.com/ce/ssh/README.html)]
- You know how to resolve merge conflicts [[4](https://confluence.atlassian.com/bitbucket/resolve-merge-conflicts-704414003.html)]

## Playing nicely with others

- You know at least one Git workflow / branching model (it should be relevant to your organization/company etc). My personal favourite is [[5](http://nvie.com/posts/a-successful-git-branching-model/)]
- You know the **dangers** of ` git push --force `
and know it's a good idea to be super careful with it [[6](https://developer.atlassian.com/blog/2015/04/force-with-lease/)]. Bonus point if you know about `git push --force-with-lease` [[7](http://movingfast.io/articles/git-force-pushing/)]
- You know how to write a good commit message [[8](http://chris.beams.io/posts/git-commit/)]

## Using Git for debugging

- You have an idea how to use `git bisect` [[9](https://git-scm.com/docs/git-bisect)]
- You know how to use `git blame` and you know it's **not** a tool for guilt tripping other developers [[10](http://alblue.bandlem.com/2011/07/git-tip-of-week-assigning-blame.html)]

## Tools etc.

- You know what Git hooks are [[11](http://githooks.com/)]
- You know how to efficiently use `git diff` between commits, branches, files staged for commit etc. [[12](https://git-scm.com/docs/git-diff)]
- You know what **submodules** are and how to efficiently use them [[13](https://chrisjean.com/git-submodules-adding-using-removing-and-updating/)]

# Wrapping up

If you know all the concepts listed above then you know Git pretty well! The knowledge you have should be enough to easily get you going on most problems you will encounter when using Git. Of course you will find some challanging problems every now and then but with your Git super powers you will not make too much of a mess in your repositories.

It's more than likely that I forgot to mention some important git skills and therefore I'm planning to update this

## Grab all the links!
1. [https://git-scm.com/docs/gitignore](https://git-scm.com/docs/gitignore)
2. [https://git-scm.com/book/en/v2/Getting-Started-First-Time-Git-Setup](https://git-scm.com/book/en/v2/Getting-Started-First-Time-Git-Setup)
3. [https://docs.gitlab.com/ce/ssh/README.html](https://docs.gitlab.com/ce/ssh/README.html)
4. [https://confluence.atlassian.com/bitbucket/resolve-merge-conflicts-704414003.html](https://confluence.atlassian.com/bitbucket/resolve-merge-conflicts-704414003.html)
5. [http://nvie.com/posts/a-successful-git-branching-model/](http://nvie.com/posts/a-successful-git-branching-model/)
6. [https://developer.atlassian.com/blog/2015/04/force-with-lease/](https://developer.atlassian.com/blog/2015/04/force-with-lease/)
7. [http://movingfast.io/articles/git-force-pushing/](http://movingfast.io/articles/git-force-pushing/)
8. [http://chris.beams.io/posts/git-commit/](http://chris.beams.io/posts/git-commit/)
9. [https://git-scm.com/docs/git-bisect](https://git-scm.com/docs/git-bisect)
10. [http://alblue.bandlem.com/2011/07/git-tip-of-week-assigning-blame.html](http://alblue.bandlem.com/2011/07/git-tip-of-week-assigning-blame.html)
11. [http://githooks.com/](http://githooks.com/)
12. [https://git-scm.com/docs/git-diff](https://git-scm.com/docs/git-diff)
13. [https://chrisjean.com/git-submodules-adding-using-removing-and-updating/](https://chrisjean.com/git-submodules-adding-using-removing-and-updating/)
