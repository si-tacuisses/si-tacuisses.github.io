---
layout: post
title: "Wolfram Mathemtica for Economists - Tutorial - Functional Programming"
modified:
categories: blog
excerpt: No excerpt yet
tags: []
image:
  feature:
  credit:
  creditlink:
date: 2015-05-16T21:57:36+02:00
---

There are a myriad of programming languages, strongly typed, weakly types, high level, low level, imperative, procedural, object orineted and so on. Mathematica is high level, dynamically typed, _funtional_ programming language.
Functional means in short that _functions_ are prime citizens. More specifically this means that the philosophy of mathematica is built around the idea that   (..... more detail on functional proramming)

- no side effects

If you have previous programming experience, you know about loop constructs (i.e. for and while loops). There are `For`, `While` and `Do` functions avaible in matheamtica if you ever need them. However if you want to do things the mathematica way and see how powerfull the idea of functional programming is, I encourage you to try and come up with solutions to problems using functional programming.

# Table

One of the most central functions you will need repeatedly is `Table`. This function eliminates for a large class of tasks the need to use `For` loops.
`Table` takes as argument a function and applies to it iteratively all elements in the specified range(s) and outputs a list a matrix or an even higher dimensional array.
Lets illustrate how `Table` works using `Cos`. 

```
In[1]   Table[ Cos[i], {i,0,Pi}]
Out[1]  {1, Cos[1], Cos[2], Cos[3]}
```

You see that `Table` has "sumbstituted" into `Cos[i]` the value for `i` which go from `0` to `Pi`. Notice that Mathematica has not evaluated the individual `Cos`. This happend since evaluating a transcendental function on an exact value (i.e. `Integer`) would lead to loss of precision.
Something els is odd. We specified that the last value should be `Pi`, but we have only obtained values up to `3`. The reason this happend is that the iterator `i` goes from `0` to `Pi` in steps of `1`. This means that `i` takes on the values `{0,1,2,3}`. 

```
ListPlot[Table[ Cos[i], {i,0,Pi}]]
```

If we were to plot this result like this we would see that the it does not look like the plot of a hormonic. Obviously we did not plot enough points to observe the  

```
In[2]   Table[Cos[i], {i, 0, Pi, .5}]
Out[2]  {1., 0.877583, 0.540302, 0.0707372, -0.416147, -0.801144, -0.989992}
```


```
In[3]   Table[{i, Cos[i]}, {i, 0, Pi, 1}]
Out[3]  { {0, 1}, {1, Cos[1]} , {2, Cos[2]}, {3, Cos[3]} }
```





