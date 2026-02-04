# 1.2. Length-And-Dot-Products
***
[[Introduction_to_Linear_Algebra_5th_Edition_2016_Gilbert_Strang.pdf#page=31&selection=66,0,68,20|(Recommended) Draw a parallelogram]]

[[Introduction_to_Linear_Algebra_5th_Edition_2016_Gilbert_Strang.pdf#page=31&selection=239,0,272,26|Pick any numbers that add to x+ y+ z = 0. Find the angle between your vec tor v = (x, y, z) and the vector w = (z, x, y). Challenge question: Explain why v · w///v// 1/wll is always-½-]]

This problem is solved by multiplying numerator by $2$ and adding-subtracting $x^{2} + y^{2} + z^{2} - x^{2} - y^{2} - z^2$
What yields
$$\begin{align}
\frac{\overbrace{ (x + y + z)^{2} }^{0} - x^{2} - y^{2} - z^{2}}{2(x^{2} +y^{2} + z^{2})} = -\frac{1}{2}
\end{align}$$

# 1.3. Matrices
***
[[Introduction_to_Linear_Algebra_5th_Edition_2016_Gilbert_Strang.pdf#page=79&selection=57,0,79,2|If AB = I and BC = I use the associative law to prove A = C.]]
$$\begin{align}
AB = BC  \\
A(AB) = (AB)C  \\
AI = IC \\
A = C
\end{align}$$

###### Block-Multiplication
***
[[Introduction_to_Linear_Algebra_5th_Edition_2016_Gilbert_Strang.pdf#page=85&selection=4,0,33,19|Example 3 (Important special case) Let the blocks of A be its n columns. Let the blocks of B be its n rows. Then block multiplication AB adds up columns times rows:]]


[[Introduction_to_Linear_Algebra_5th_Edition_2016_Gilbert_Strang.pdf#page=101&selection=5,0,19,2|2.5 B Three of these matrices are inve1iible, and three are singular. Find the inverse when it exists. Give reasons for noninvertibility (zero determinant, too few pivots, nonzero solution to Ax= 0) for the other three. The matrices are in the order A, B, C, D, S, E:]]