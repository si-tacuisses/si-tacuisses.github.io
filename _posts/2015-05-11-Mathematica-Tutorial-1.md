---
layout: post
title: Tutorial - Wolfram Mathematica for Economists - Part 1
---

I am writing a series on how to use [Wolfram Mathematica](http://www.wolfram.com/mathematica/) for economic research, take notes and do exploratory data analysis.
I will focus in the examples on economic applications and some widely used models to illustrated the Mathematica's efficiency.



Mathematica is a very powerful and expressive programming language, which I use on a daily basis to do my research. It is unrivalled in Symbolic computation and it is very fast to test ideas, sketch a simple model or review results in journals.
Once you see how powerful this tool is for note taking in maths heavy classes you will appreciate it too.

However, before dive into some interesting applications of Mathematica to real problems, let's get acquainted with he basics.

## First Things First

Before we  start with some economics examples to get acquainted with Mathematica we need to understand the most important parts of the language and how they tie together. We look at the basic types `Integer`, `Rational`,`Real`, `String` `Complex` and  `List`  and how to defined and use basic functions.

### Numbers

Let's look at `Integer`s first in the followint example. To evaluate the `1+1` press `Shift` and `Enter` and you should get `2`.

```Mathematica
In[1]   1 + 1
Out[2]  2
```

Mathematica avoids conversion of types to more general types whenever possible to avoid any loss of precision (i.e. 1/3 is not transformed from a rational to a real number since this would reduce precision).
 Integers as far as possible and does not coerce them to `Real`s (i.e. Real Numers or floating point Numbers). In fact Mathematica tries to keep percision as high as possible by keeping `Integer`s and `Rational`s (i.e. Fractions) throughout the evaluation process.
Any of these two can be coerced to a `Real` if eitehr a floating point number is used in the operation or it is explicitelly transformed using `N`

```Mathematica
In[1]   1 + 1/2
Out[1]  3/2
In[2]   1 + 0.5
Out[2]   1.5
In[3]   N[3/2]
Out[3]  1.5
```

The basic binary operators such as `+` , `-`, `*` and `/` are used just as you use them in any other context no brackets, braces or other programming syntax is involved[^defbinary].
Howeve if you want to call a function which is not one of these you will need to call them using function syntax. By function syntax I mean to call for example \\(\ln(x)\\) which takes one argument using the mma function `Log[x]`.
```Mathematica
In[1]   Log[1]
Out[1]  0
```
Some things to note here. Official mma functions start with a capital letter and are complete words in the CammelCase style, unlike MATLAB where functions are lower case and excessively shortened (e.g. num2str). Furthermore unlike MATLAB, Python, R, C/C++ and many other languages the arguments passed to a function are enclosed in square brackets `[ ]`. Parenthesis `( )` are used exclusively for grouping and define the order of operations.

### Lists
Vectors, as you might already know, are simply Lists and in Mathematica vectors are effectively called `List`.  Conversly a matrix is a vector of vectors and as such matrices are implemented in Mathematica as lists of lists.  And higher order structures, say an array with 3 dimensions is a list of lists of lists. I guess you get the point.
A list is a set of Expressions in curly braces `{x1,x2,...,xn}`.
Since it is conceptually equal to a vector in linear algebra you can do the basic operations directly on them. 

```mathematica
In[1]  {1, 2, 3} + {1, 2, 3}
Out[1] {2, 4, 6}
In[2]  2*{1,2,3}
Out[2] {2,4,6}
In[3]  {1, 2, 3}.{1, 2, 3}
Out[3] 14
```

Lists are a central part of Mathematica and a lot of function parameters are supplied as lists.
### Functions
One of the most widely used functional Production Functions is [Cobb-Douglas][wikiCobb]. Lets look at this omnipresent function.
\\[
Y=F(L,K)=A L^\alpha K^\beta
\\]

Usually in textbook examples it is assumed that the returns to scale
are constant. This means effectively that \\(\beta=1-\alpha\\) and
both are positive. Let's now define this function in Mathematica. A
function in mathematica takes the following form:

```
<FuncName>[var1_,var2_]:= <functionBody>
```

Here `<FuncName>` is the name you assign to the function, then in the square brackets we name the arguments here `var1` and and `var2`. Note the underscore after the variable name. This underscore is necessary as it tells Mathematica "I want to take this and only this argument found here and name it `var`" [^1] . For now just remember that every argument on the lhs of the definition must be defined with an underscore (`_`) after the name and can then be used in the rhs without the underscore.
Then we have the `:=` which effectively means "take the variables on the left and do something on the right", unlike `=` the `:=` operator tells Mathematica to not remember the rhs as is, but to evaluate it every time it is called.
Here we define our function. 

```mathematica
In[1]   CobbDouglas[L_,K_,A_,a_,b_]:=   A * L^a * K^b
In[2]   CobbDouglas[L_,K_,A_,a_]:= CobbDouglas[L,K,A,a,1-a]
```

A lot happened here, so lets look at what we just wrote. We defined a function called `CobbDouglas` on line 1. This function takes 5 arguments and assigns them to the rhs to compute a value. As you can see we have here both `a` and `b` which corresponds to the general case of a cobb douglas.
On line 2 we define the special constant returns to scale variant. Note that we use the same function name `CobbDouglas`  however with only 4 arguments. You can see on the right hand side this is nothing more than to say that if `CobbDouglas`  is called with only 4 arguments we assume that we deal with a constant returns to scale situation. We have given the same name to two different functions varying only on the number (and possibly type) or arguments. [Overloading](http://en.wikipedia.org/wiki/Operator_overloading) as it is called is a way to define a function which behaves differently depending on what parameters it obtains.

Now lets move to a more fun application of this function. 
Let's plot the surface of our `CobbDouglas` function for all \\(L\\) and \\(K\\) from 0 to 1, holding \\(A\\) and \\(\alpha\\) fixed at 1 and 0.5 respectively.
We use the build-in [Plot3D](https://reference.wolfram.com/language/ref/Plot3D.html) function to do this.

```Mathematica
Plot3D[ CobbDouglas[l, k, 1, .5], {l, 0, 1}, {k, 0, 1},
    AxesLabel -> {"L","K","Y"}, 
    ColorFunction -> "DarkRainbow"],
    MeshFunctions -> {#3 &}]
```

![cobbDouglas]({{ site.baseurl }}/images/cobb_douglas.png "CobbDouglas")



[^1]: The underscore is part of Mathematica's internal pattern matching. The pattern matching is very powerful approach when defining more complex functions. Take a look at the [manual page](https://reference.wolfram.com/language/guide/Patterns.html)






