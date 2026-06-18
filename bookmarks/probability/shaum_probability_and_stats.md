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
***

[[shaum_probability_and_stats.pdf#page=40&selection=9,0,22,1|(a) A shelf contains 6 separate compartments. In how many ways can 4 indistinguishable marbles be placed in the compartments? (b) Work the problem if there are n compartments and r marbles. This type of problem arises in physics in connection with Bose-Einstein statistics.]]

First thought was 
$$\begin{align}
\frac{6^4}{4!}
\end{align}$$
But dividing by $4!$ assumes every indistinguishable arrangement corresponds exactly to $4!$ labeled arrangements. Which is not true when all marbles end up in one compartment, more strictly all marbles must be in different compartments.

Right solution: There're 4 start corresponding to 4 marbles and 5 bars which corresponding to 6 compartments. Thereof we need to choose 5 indices for 5 bars out of 4 + 5 indices.
$$\begin{align}
{4 + 6 - 1 \choose 6 - 1} = 126
\end{align}$$
***

[[shaum_probability_and_stats.pdf#page=40&selection=26,0,43,1|(a) A shelf contains 6 separate compartments. In how many ways can 12 indistinguishable marbles be placed in the compartments so that no compartment is empty? (b) Work the problem if there are n compartments and r marbles where r n. This type of problem arises in physics in connection with Fermi-Dirac statistics]]

This problem is much similar to above. Consider having 5 marbles
$$\begin{align}
\star \star \star \star \star 
\end{align}$$
to arrange them along 3 compartments we must choose 2 indices along 4 indices _(we can't pick leading and trailing, because compartments are empty then)_. We can't pick index twice so:
$$\begin{align}
5 - 1 \choose 3 - 1
\end{align}$$
Thereof problem above is solved as:
$$\begin{align}
12 - 1 \choose 5 - 1 = 462
\end{align}$$
general solution is
$$\begin{align}
n - 1 \choose r - 1
\end{align}$$
***
[[shaum_probability_and_stats.pdf#page=40&selection=60,0,60,98|Find the probability that in a game of bridge (a) 2, (b) 3, (c) all 4 players have a complete suit]]

_(a)_ It a little bit tricky. Distributing 13 cards to each player is 
$$\begin{align}
13, 13, 13, 13 \choose 52
\end{align}$$
But it actually contains each permutation of groups. For example first player get clubs and the second hearts, then there's also are permutations when first get hearts and second got hearts. There're $4!$ such permutation. Then answer is
$$\begin{align}
\frac{_{4}P_{2} {26 \choose 13} {13 \choose 13}}{{52 \choose 13, 13, 13, 13}}
\end{align}$$
Now numerator contains $4!$ permutations and the denominator contains $4!$ permutations thereof the answer is
$$\begin{align}
\frac{12}{{52 \choose 13}{39 \choose 13}}
\end{align}$$

_(b)_ and _(c)_ solved in the same way.


# Chapter 1.2
***
[[shaum_probability_and_stats.pdf#page=73&selection=234,0,250,1|A floor has parallel lines on it at equal distances l from each other. A needle of length a  l is dropped at random onto the floor. Find the probability that the needle will intersect a line. (This problem is known as Buffon’s needle problem.)]]

Interesting problem, it's not hard to understand how to solve this in terms of double integral, but hard to make proper constraints.
***


current: [[shaum_probability_and_stats.pdf#page=80&selection=269,0,281,76|A cylindrical stream of particles, of radius a, is directed toward a hemispherical target ABC with center at O as indicated in Fig. 2-26. Assume that the distribution of particles is given b]]

answers: [[shaum_probability_and_stats.pdf#page=83&selection=118,0,118,4|2.93]]


# Chapter-3
***
May be interesting to find out moments of [[shaum_probability_and_stats.pdf#page=110&selection=7,4,9,5|Use the generating function of (a) to find the first four moments about the origin.]] To do so we need to expand $e^{2t}$ in numerator of mgf and match with terms of taylor expansion of moment generating function. 
***

Pretty neat to understand how to apply L'Hopital rule here. Define $x = \frac{w}{\sqrt{ n }}$ then $n = (\frac{w}{x})^2$ and $x \to 0$ when $n \to \infty$. Apply L'hopital rule twice, then exponentiate to get answer.
[[shaum_probability_and_stats.pdf#page=110&selection=87,0,96,1|Prove that as the characteristic function of Problem 3.73 approaches (Hint: Take the logarithm of the characteristic function and use L’Hospital’s rule.)]]
***


# Chapter-4
***
**problem:**
[[shaum_probability_and_stats.pdf#page=157&selection=108,0,109,14|Student’s t distribution]]

**solution**:
[[shaum_probability_and_stats.pdf#page=159&selection=27,0,27,5|4.116]]

Side read before continuing exercises
[[gamma_chi_student_f_distributions.pdf#page=2&selection=130,0,151,5|Let us compute the kth moment of gamma distribution. We have,]]

# Chapter-5
***
[[shaum_probability_and_stats.pdf#page=166&selection=10,0,10,45|Sampling Distribution of Differences and Sums]]

**Current**: 
[[shaum_probability_and_stats.pdf#page=202&selection=26,0,26,5|5.130]]

**answer**: 
[[shaum_probability_and_stats.pdf#page=203&selection=304,0,304,5|5.130]]

***
[[shaum_probability_and_stats.pdf#page=202&selection=16,0,19,5|Certain tubes produced by a company have a mean lifetime of 900 hours and a standard deviation of 80 hours. The company sends out 1000 lots of 100 tubes each. In how many lots can we expect (a) the mean lifetimes to exceed 910 hours, (b) the standard deviations of the lifetimes to exceed 95 hours? What assumptions must be made?]]

Interesting to understand how to solve _(b)_. It actually asks for
$$\begin{align}
P(S_{Y} > 95^2)
\end{align}$$
where $Y$ is sample of size $n = 100$
$$\begin{align}
P(S_{Y} > 95^2) \\
= P\left(  \sum \frac{{(X_{i} - \overline{X})^2}}{n} > 9025 \right) \\
= P\left(  \sum \frac{{(X_{i} - \overline{X})^2}}{\sigma^2} > 9025 \cdot \frac{100}{\sigma^2} \right) \\
= P(\chi^2_{99} > 141) \\
= 0.00358
\end{align}$$
where left hand side sum is Chi squared distribution with $99$ degrees of freedom. Thereof answer is $1000 * P(S_{Y} > 95^2) \approx 4$
***

[[shaum_probability_and_stats.pdf#page=202&selection=28,0,32,6|On a citywide examination the grades were normally distributed with mean 72 and standard deviation 8. (a) Find the minimum grade of the top 20% of the students. (b) Find the probability that in a random sample of 100 students, the minimum grade of the top 20% will be less than 76.]]
It is hard to understand what expression to solve for in _(b)_. Actually we can compute probability of single grade to be less than 76
$$\begin{align}
P(X \leq 76) = P\left( Z \leq \frac{72 - 76}{8}\right) = 0.6915
\end{align}$$
And then we need to compute probability of $Y = \sum X_{i}$ be greater then $80$
$$\begin{align}
P(Y > 80) = P\left( Z > \frac{80 - 69}{\sqrt{ 100 \cdot 0.6915 \cdot 0.3085 }} \right) \\
= P(Z > 2.38) \\
\approx 0.009
\end{align}$$

# Chapter-6
***
**current:**
[[shaum_probability_and_stats.pdf#page=220&selection=2,0,3,1|6.58.]]

**answer**:
[[shaum_probability_and_stats.pdf#page=221&selection=54,0,54,5|6.58.]]


# Chapter-7
***
- [[shaum_probability_and_stats.pdf#page=226&selection=72,3,72,29|DIFFERENCES OF PROPORTIONS]]
- [[shaum_probability_and_stats.pdf#page=227&selection=0,3,0,23|DIFFERENCES OF MEANS]]
- [[shaum_probability_and_stats.pdf#page=230&selection=218,0,218,32|Yates’ Correction for Continuity]]
- [[shaum_probability_and_stats.pdf#page=231&selection=14,0,14,26|Coefficient of Contingency]]

[[shaum_probability_and_stats.pdf#page=262&selection=20,0,27,12|Use the result of Problem 7.61 to show that 2, as defined by (21), page 220, is approximately chi-square distributed.]]


[[shaum_probability_and_stats.pdf#page=268&selection=25,0,25,5|7.109]]
1. Compute marginal probabilities of P(D) and P(!D).
2. Compute expected frequencies from marginal for P(V) and P(Not V)
3. Compute Chi squared statistic for Chi squared with $(h - 1)(k - 1)$ degrees of freedom.

**current**: 
[[shaum_probability_and_stats.pdf#page=270&selection=81,0,81,5|7.122]]

**answer:**
[[shaum_probability_and_stats.pdf#page=273&selection=68,0,68,5|7.122]]

# Chapter-8
***
- [[shaum_probability_and_stats.pdf#page=277&selection=59,0,59,66|The Least-Squares Line in Terms of Sample Variances and Covariance]]
- [[shaum_probability_and_stats.pdf#page=277&selection=116,0,116,26|The Least-Squares Parabola]]
- [[shaum_probability_and_stats.pdf#page=278&selection=27,0,27,19|Multiple Regression]]
- [[shaum_probability_and_stats.pdf#page=278&selection=91,0,91,26|Standard Error of Estimate]]
- [[shaum_probability_and_stats.pdf#page=279&selection=46,0,46,34|The Linear Correlation Coefficient]]
- [[shaum_probability_and_stats.pdf#page=279&selection=67,0,67,19|explained variation]]
- [[shaum_probability_and_stats.pdf#page=280&selection=55,0,55,35|Generalized Correlation Coefficient]]
- [[shaum_probability_and_stats.pdf#page=280&selection=105,0,105,16|Rank Correlation]]
- [[shaum_probability_and_stats.pdf#page=282&selection=25,0,25,41|Probability Interpretation of Correlation]]
- [[shaum_probability_and_stats.pdf#page=282&selection=58,0,58,29|Sampling Theory of Regression]]
- [[shaum_probability_and_stats.pdf#page=283&selection=18,0,18,30|Sampling Theory of Correlation]]

**current:**
[[shaum_probability_and_stats.pdf#page=309&selection=11,0,11,4|8.53]]


# Chapter-9
***
- [[shaum_probability_and_stats.pdf#page=323&selection=25,0,27,4|One-Way Classification or One-Factor Experiments]]
- [[shaum_probability_and_stats.pdf#page=324&selection=6,0,8,13|Total Variation. Variation Within Treatments. Variation Between Treatments]]
- [[shaum_probability_and_stats.pdf#page=324&selection=85,0,85,41|Shortcut Methods for Obtaining Variations]]
- [[shaum_probability_and_stats.pdf#page=324&selection=124,0,124,50|Linear Mathematical Model for Analysis of Variance]]
- [[shaum_probability_and_stats.pdf#page=325&selection=89,0,89,33|Expected Values of the Variations]]
- [[shaum_probability_and_stats.pdf#page=326&selection=10,0,10,31|Distributions of the Variations]]
- [[shaum_probability_and_stats.pdf#page=326&selection=75,0,76,45|The F Test for the Null Hypothesis of Equal Means]]
- [[shaum_probability_and_stats.pdf#page=326&selection=146,0,146,27|Analysis of Variance Tables]]
- [[shaum_probability_and_stats.pdf#page=327&selection=5,0,5,49|Modifications for Unequal Numbers of Observations]]
- [[shaum_probability_and_stats.pdf#page=327&selection=370,0,370,48|Two-Way Classification or Two-Factor Experiments]]
- [[shaum_probability_and_stats.pdf#page=328&selection=180,0,180,37|Variations for Two-Factor Experiments]]
- [[shaum_probability_and_stats.pdf#page=329&selection=5,0,5,47|Analysis of Variance for Two-Factor Experiments]]
- [[shaum_probability_and_stats.pdf#page=330&selection=559,0,559,39|Two-Factor Experiments with Replication]]
- [[shaum_probability_and_stats.pdf#page=332&selection=89,0,89,19|Experimental Design]]

**current**: 
[[shaum_probability_and_stats.pdf#page=343&selection=32,0,32,13|Latin squares]]
