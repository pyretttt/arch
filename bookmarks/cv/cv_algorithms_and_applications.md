# 8. Image-Stitching
***
!**Review** [[Computer Vision Algorithms and Applications (Texts in Computer Science) [2022] Richard Szeliski.pdf#page=422&selection=37,0,37,21|Uncertainty weighting]] refers to [[Computer Vision Algorithms and Applications (Texts in Computer Science) [2022] Richard Szeliski.pdf#page=471&selection=203,0,203,17|Parametric motion]] for covariance estimate for patch based matching.

[[Computer Vision Algorithms and Applications (Texts in Computer Science) [2022] Richard Szeliski.pdf#page=424&selection=60,0,110,54|For the case of our 2D translation+rotation, we end up with a 3 × 3 set of normal equations in the unknowns (δtx, δty , δθ). An initial guess for (tx, ty , θ) can be obtained by fitting a four-parameter similarity transform in (tx, ty , c, s) and then setting θ = tan−1(s/c). An alternative approach is to estimate the translation parameters using the centroids of the 2D points and to then estimate the rotation angle using polar coordinates (Exercise 8.3).]]
[[Computer Vision Algorithms and Applications (Texts in Computer Science) [2022] Richard Szeliski.pdf#page=763&selection=204,79,204,80|.]]
