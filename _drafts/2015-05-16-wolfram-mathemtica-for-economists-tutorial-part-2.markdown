---
layout: post
title: "Wolfram Mathemtica for Economists - Tutorial - Part 2"
modified:
categories: blog
excerpt:
tags: [tutorial, Mathematica, ]
image:
  feature:
  credit:
  creditlink:
date: 2015-05-16T21:15:18+02:00
math: true
core: true
---

In the last [post](insertLink) we looked at some of the most important constructs and data-types in Mathematica. Now that we know how to define a simple function and know what `Lists`s, `Integer`s and `Real`s are, we look at one of the main applications of mathematica in research: *plotting*.

*table of contents*
{:toc}

Mathematica has very powerful plotting capabilities and functions, which produce quite good looking figures. The unprocessed output is not exactly publication quality, but for a few keystrokes you get quite the bang for the buck. If you want to prepare some journal grade figures you can do that with a little experience and some special [packages][^pack] rivalling even the likes of [TikZ][tikz] and [PGF][pgf].

# ListPlot

At the heart of Mathematica's plotting framework there is `ListPlot`.
This function takes as arguments a list and outputs a plot. This list can be either simple (i.e. a sequence of numbers) like this.

```
In[1]  cosList = Cos[Range]
```















[tikz]: http://www.google.com
[pgf]: http://www.google.com

[^pack]: I will cover this more advanced topic later in the series. However if you can't wait till then, I recommend you check out the package _MaTeX_ by .... This presupposes some knowledge of \\(\TeX\\) and snoop around on [mathematica.se](http://mathematica.stackexchange.com)