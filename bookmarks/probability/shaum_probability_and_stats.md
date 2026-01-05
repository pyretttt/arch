# Chapter 1
***
Exercise about secretary: [[shaum_probability_and_stats.pdf#page=34&selection=176,0,186,3|An inefficient secretary places n different letters into n differently addressed envelopes at random. Find the probability that at least one of the letters will arrive at the proper destination.]]
***

Distinct birthday paradox: [[shaum_probability_and_stats.pdf#page=35&selection=31,0,42,20|Find the probability that n people (n 365) selected at random will have n different birthdays.]]
***

[[shaum_probability_and_stats.pdf#page=38&selection=11,0,11,86|How many different three-digit numbers can be made with 3 fours, 4 twos, and 2 threes?]]

Basically it can be solved by general formula -counting by cases on the digit pattern (all same, two same + one different, all different)

But there're it's easier to just note that there're
$$\begin{align}
3^3=27
\end{align}$$
ways to form 3 digit number out of 3 distinct digits, but we can't form number $222$, so there're actually $26$ ways to do so.
***

[[shaum_probability_and_stats.pdf#page=38&selection=15,0,16,84|In how many ways can 3 men and 3 women be seated at a round table if (a) no restriction is imposed, (b) 2 particular women must not sit together, (c) each woman is to be between 2 men?]]

_(A)_ We care only about how people are arranged to each other, so that if move each person to adjacent sit, it is the same arrangement of people. So that we pick first person and arrange remaining 5 across remaining sits. Hence, $5! = 120$ ways to do it. 

_(b)_ We know that there're $120$ ways to arrange 6 person. Let merge two women into 1 therefore there $4!$ to arrange remaining $5$ persons and $2$ to permute order of this merged woman. Therefore we have $120 - 4! \cdot 2 = 72$ ways to do so. 

_(C)_. Let's also fix one man somewhere, it doesn't matter, let say at index $i$. Then there're $2!$ ways to arrange men at indices $i + 2, i + 4$ and $3!$ ways to arrange women at indices $i + 1, i + 3, i+5$ resulting in total $3! 2! = 12$ ways.
***

[[shaum_probability_and_stats.pdf#page=38&selection=87,0,91,1|Find the number of (a) combinations and (b) permutations of 4 letters each that can be made from the letters of the word Tennessee.]]

Part _(a)_ is trivial. There's $1$ way to pick all the same letters _(eeee)_. There're 3 ways to pick 3 same letters and 1 different _(eeet, eees, eeen)_. There're 9 ways to pick 2 same and 2 diff _(eest, eesn, eetn, sset, ssen, sstn, ...)_. There're 3 ways to pick 2 same and another pair _(eenn, eess, ssnn)_. And there 1 ways to pick all different. Hence
$$\begin{align}
1 + 3 + 9 + 3 + 1 = 17
\end{align}$$

Part _(b)_. Let's permute combinations from part _(a)_. There're 1 way to permute all the same letters. There're $4$ ways to permute $3$ same letter and 1 different, so we have $3 \cdot 4 = 12$ arrangements. There're $4 \cdot 3$ ways to permute 2 same and 2 different letters, thereof $12 \cdot 9 = 108$ arrangements. There're $\frac{4!}{2!2!}$ ways to permute 2 same and another two same letters, thereof $6 \cdot 3 = 18$ total arrangements. And $4$ different letters can be arranged in $4! = 24$ ways. Hence
$$\begin{align}
1 + 12 + 108 + 18 + 24 = 163
\end{align}$$

**Next to solve:** [[shaum_probability_and_stats.pdf#page=39&selection=96,0,99,9|1.93. A pair of dice is tossed repeatedly. Find the probability that an 11 occurs for the first time on the 6th toss.]]