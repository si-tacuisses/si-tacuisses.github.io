---
layout: post
title: "Vietnamese Snake Puzzle"
modified:
categories: blog
excerpt:
tags: [puzzle, mathematica]
image:
  feature:
  credit:
  creditlink:
date: 2015-05-24T17:18:37+02:00
math: true
mma: true
---


As of late the intertubes are pretty fond of math puzzles, and as it seams especially of the "Asian kids can solve this" variety. So after the blogosphere, twittersphere and quite possibly the lithosphere took on the [Charil's Birthday Problem][charil] it has moved on to the [Vietnamese Snake][vsnake].
The [Vietnamese snake][vsnake] is a maths puzzle presented to Vietnamese eight year olds as [Alex Bellos][vsnake] describes it in his guardian [article][vsnake].

The students were presented with the following figure and asked to insert all numbers from 1 through 9 without repetition. Or put in other words, insert every number from 1 through 9 exactly once in the figure with the goal to obtain the required result of 66.

![Vietnamese Snake Puzzle](http://i.guim.co.uk/static/w-700/h--/q-95/sys-images/Guardian/Pix/pictures/2015/5/20/1432109324993/f7e7f4a5-b59c-4580-88f4-ddc609584d19-bestSizeAvailable.png)

Before I move on to present a brute-force method to enumerate all possible solutions, I encourage you to try it on your own. If you google it or have a look in the comments section of the original article you will come up with some interesting solution approaches and the flame war on the number of possible solutions (hint: it's not 148).

Ready?

Now that you had a go at it and probably came up with a solution or possibly all solutions. I present a brute-force solution for Mathematica.
I assume here that you now the basics of the [Wolfram Language]({% post_url /blog/2015-05-16-mathematica-tutorial %}), however I present my solution approach step by step in a tutorial style.

The above snake can be rewritten as an equation where the blanks are substituted with variables. Here I choose to name them \\( \{a,b,...,i \}\\) and obtain \\eqref{eq:1}.

\\begin{equation}
	a + \frac{13 b}{c} + d + 12 e - f - 11 + \frac{g h}{i} - 10 = 66
	\label{eq:1}
\\end{equation}

To work better in Mathematica with this expression we create the following function 

```
snake[args_List]:= Module[{a,b,c,d,e,f,g,h,i},
	{a,b,c,d,e,f,g,h,i} = args;
	a + (13 b/c) + d + 12 e - f - 11 + (g h/i) - 10
]
```

It takes an argument called `args` and checks if it is a `List`. Then we localize the values of the variables by using `Module`. The first argument to `Module` is a list of variables which are defined only within this [scope][scoping]. We do that to avoid pollution of the global namespace[^ft1]. We unpack the variables from `args` and finally compute the function we are interested in. The result of the last expression is considered by Mathematica to be the return value.

Next, since the problem states that we need to use every number exactly once we construct a matrix containing all possible permutations as row entries. Note that for 9 distinct objects the number of possible combinations is 9!=362,880. To do this we use the build-in function `Permutations` as seen below.

```
permutations = Permutations[Range@9, {9}];
```

Now we need to compute the value of `snake` for every row in `permutations`. We do this with `Map` or its shorthand `/@`. Don't forget the `;` after the expression or you will have a lot of output on your screen.

```
values	= Map[snake, permutations];
values	= snake/@permutations;
```

We have now all the possible values for snake on the "legal" arguments. Now it is time to look at which of these values are equal to our desired output `66`. The function `Position` comes in very handy for this task. This function looks over the entire list and returns the position of the entries which match the pattern passed to it as  second argument. The pattern we are interested in is `66`.

```
positions	= Flatten@Position[values, 66];
```

The only thing left to do now it to filter out the valid solutions.

```
solutions	= Map[permutations[[#]]&, positions]
```

Below you will find the list of all solutions. Note that there are exactly 136 solutions and not any other number. The reason some [other](vsnake) people have come up with a different number is that in their brute force approach using a different language a problem of precision arises. For example 66.00000000000001 would be considered a valid solution even though it is not. Mathematica avoid all of this by using exact fractions and not floating point numbers.

If you feel that this is a pretty long solution for such a simple problem, you can condense this approach down to the length of a tweet, a pretty ugly tweet but a tweet nonetheless. In fact you can try to tweet this line to @wolframtap and the Wolfram twitter bot will reply with the result.

```
m=Permutations[Range@9,{9}];m[[#]]&/@Position[a+13b/c+d+12e-f+g*h/i/.Thread[{a,b,c,d,e,f,g,h,i}->m[[#]]]&/@Range@Length[m],87]
```

# Some interesting properties

If we plot the number of solutions for a given target value (i.e. change 66) we can observe the following pattern.

```
distribution = {#, Length@Position[values, #]} & /@ Range[220];
ListPlot[distribution, 
	PlotTheme -> "Scientific",
	FrameLabel -> {"Target Value", "# of solutions"}
	]
```

![snake_distribution]({{ site.baseurl }}/images/snakedistribution.svg "Snake Distribution")
{: .imageoutput}

The lowest number of solutions which is not 0 is 4. I leave it to you to find which.


|solution number|a|b|c|d|e|f|g|h|i|
|-:|:-|:-|:-|:-|:-|:-|:-|:-|:-|
|1|1|2|6|4|7|8|3|5|9|
|2|1|2|6|4|7|8|5|3|9|
|3|1|3|2|4|5|8|7|9|6|
|4|1|3|2|4|5|8|9|7|6|
|5|1|3|2|9|5|6|4|7|8|
|6|1|3|2|9|5|6|7|4|8|
|7|1|3|4|7|6|5|2|9|8|
|8|1|3|4|7|6|5|9|2|8|
|9|1|3|6|2|7|9|4|5|8|
|10|1|3|6|2|7|9|5|4|8|
|11|1|3|9|4|7|8|2|5|6|
|12|1|3|9|4|7|8|5|2|6|
|13|1|4|8|2|7|9|3|5|6|
|14|1|4|8|2|7|9|5|3|6|
|15|1|5|2|3|4|8|7|9|6|
|16|1|5|2|3|4|8|9|7|6|
|17|1|5|2|8|4|7|3|9|6|
|18|1|5|2|8|4|7|9|3|6|
|19|1|5|3|9|4|2|7|8|6|
|20|1|5|3|9|4|2|8|7|6|
|21|1|8|3|7|4|5|2|6|9|
|22|1|8|3|7|4|5|6|2|9|
|23|1|9|6|4|5|8|3|7|2|
|24|1|9|6|4|5|8|7|3|2|
|25|1|9|6|7|5|2|3|4|8|
|26|1|9|6|7|5|2|4|3|8|
|27|2|1|4|3|7|9|5|6|8|
|28|2|1|4|3|7|9|6|5|8|
|29|2|3|6|1|7|9|4|5|8|
|30|2|3|6|1|7|9|5|4|8|
|31|2|4|8|1|7|9|3|5|6|
|32|2|4|8|1|7|9|5|3|6|
|33|2|6|9|8|5|1|4|7|3|
|34|2|6|9|8|5|1|7|4|3|
|35|2|8|6|9|4|1|5|7|3|
|36|2|8|6|9|4|1|7|5|3|
|37|2|9|6|3|5|1|4|7|8|
|38|2|9|6|3|5|1|7|4|8|
|39|3|1|4|2|7|9|5|6|8|
|40|3|1|4|2|7|9|6|5|8|
|41|3|2|1|5|4|7|8|9|6|
|42|3|2|1|5|4|7|9|8|6|
|43|3|2|4|8|5|1|7|9|6|
|44|3|2|4|8|5|1|9|7|6|
|45|3|2|8|6|5|1|7|9|4|
|46|3|2|8|6|5|1|9|7|4|
|47|3|5|2|1|4|8|7|9|6|
|48|3|5|2|1|4|8|9|7|6|
|49|3|6|4|9|5|8|1|7|2|
|50|3|6|4|9|5|8|7|1|2|
|51|3|9|2|8|1|5|6|7|4|
|52|3|9|2|8|1|5|7|6|4|
|53|3|9|6|2|5|1|4|7|8|
|54|3|9|6|2|5|1|7|4|8|
|55|4|2|6|1|7|8|3|5|9|
|56|4|2|6|1|7|8|5|3|9|
|57|4|3|2|1|5|8|7|9|6|
|58|4|3|2|1|5|8|9|7|6|
|59|4|3|9|1|7|8|2|5|6|
|60|4|3|9|1|7|8|5|2|6|
|61|4|9|6|1|5|8|3|7|2|
|62|4|9|6|1|5|8|7|3|2|
|63|5|1|2|9|6|7|3|4|8|
|64|5|1|2|9|6|7|4|3|8|
|65|5|2|1|3|4|7|8|9|6|
|66|5|2|1|3|4|7|9|8|6|
|67|5|3|1|7|2|6|8|9|4|
|68|5|3|1|7|2|6|9|8|4|
|69|5|4|1|9|2|7|3|8|6|
|70|5|4|1|9|2|7|8|3|6|
|71|5|4|8|9|6|7|1|3|2|
|72|5|4|8|9|6|7|3|1|2|
|73|5|7|2|8|3|9|1|6|4|
|74|5|7|2|8|3|9|6|1|4|
|75|5|9|3|6|2|1|7|8|4|
|76|5|9|3|6|2|1|8|7|4|
|77|6|2|8|3|5|1|7|9|4|
|78|6|2|8|3|5|1|9|7|4|
|79|6|3|1|9|2|5|7|8|4|
|80|6|3|1|9|2|5|8|7|4|
|81|6|9|3|5|2|1|7|8|4|
|82|6|9|3|5|2|1|8|7|4|
|83|7|1|4|9|6|5|2|3|8|
|84|7|1|4|9|6|5|3|2|8|
|85|7|2|8|9|6|5|1|3|4|
|86|7|2|8|9|6|5|3|1|4|
|87|7|3|1|5|2|6|8|9|4|
|88|7|3|1|5|2|6|9|8|4|
|89|7|3|2|8|5|9|1|6|4|
|90|7|3|2|8|5|9|6|1|4|
|91|7|3|4|1|6|5|2|9|8|
|92|7|3|4|1|6|5|9|2|8|
|93|7|5|2|8|4|9|1|3|6|
|94|7|5|2|8|4|9|3|1|6|
|95|7|6|4|8|5|9|1|3|2|
|96|7|6|4|8|5|9|3|1|2|
|97|7|8|3|1|4|5|2|6|9|
|98|7|8|3|1|4|5|6|2|9|
|99|7|9|6|1|5|2|3|4|8|
|100|7|9|6|1|5|2|4|3|8|
|101|8|2|4|3|5|1|7|9|6|
|102|8|2|4|3|5|1|9|7|6|
|103|8|3|2|7|5|9|1|6|4|
|104|8|3|2|7|5|9|6|1|4|
|105|8|5|2|1|4|7|3|9|6|
|106|8|5|2|1|4|7|9|3|6|
|107|8|5|2|7|4|9|1|3|6|
|108|8|5|2|7|4|9|3|1|6|
|109|8|6|4|7|5|9|1|3|2|
|110|8|6|4|7|5|9|3|1|2|
|111|8|6|9|2|5|1|4|7|3|
|112|8|6|9|2|5|1|7|4|3|
|113|8|7|2|5|3|9|1|6|4|
|114|8|7|2|5|3|9|6|1|4|
|115|8|9|2|3|1|5|6|7|4|
|116|8|9|2|3|1|5|7|6|4|
|117|9|1|2|5|6|7|3|4|8|
|118|9|1|2|5|6|7|4|3|8|
|119|9|1|4|7|6|5|2|3|8|
|120|9|1|4|7|6|5|3|2|8|
|121|9|2|8|7|6|5|1|3|4|
|122|9|2|8|7|6|5|3|1|4|
|123|9|3|1|6|2|5|7|8|4|
|124|9|3|1|6|2|5|8|7|4|
|125|9|3|2|1|5|6|4|7|8|
|126|9|3|2|1|5|6|7|4|8|
|127|9|4|1|5|2|7|3|8|6|
|128|9|4|1|5|2|7|8|3|6|
|129|9|4|8|5|6|7|1|3|2|
|130|9|4|8|5|6|7|3|1|2|
|131|9|5|3|1|4|2|7|8|6|
|132|9|5|3|1|4|2|8|7|6|
|133|9|6|4|3|5|8|1|7|2|
|134|9|6|4|3|5|8|7|1|2|
|135|9|8|6|2|4|1|5|7|3|
|136|9|8|6|2|4|1|7|5|3|




[charil]: https://en.wikipedia.org/wiki/Cheryl%27s_Birthday
[vsnake]: http://www.theguardian.com/science/alexs-adventures-in-numberland/2015/may/20/can-you-do-the-maths-puzzle-for-vietnamese-eight-year-olds-that-has-stumped-parents-and-teachers

[scoping]: https://en.wikipedia.org/wiki/Scope_(computer_science)





[^ft1]: For example we find that `a` has a different value then we expect when we deal with some other function and even an other notebook, since both notebooks use the same math-kernel session


