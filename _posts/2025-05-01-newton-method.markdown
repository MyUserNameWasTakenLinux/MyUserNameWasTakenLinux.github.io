---
layout: post
title:  "Higher-Order Newton Methods"
date:   2025-05-03 12:09:08 -0700
categories: numerical-methods
math: true
---

The paper *Higher-Order Newton Methods with Polynomial Work per Iteration* by Ahmadi et al. presents a generalization of Newton's method that uses the dth-order Taylor approximation of the function that is to be minimzed. The function may be of multiple variables. The most obvious way of extending the classical Newton's Method to use higher-order Taylor approximations does not work, because it involves solving NP-hard problems as subtasks (for example finding the global minimum of an even degree polynomial that is not of degree 2).

The algorithm proposed by the paper goes as follows. Compute the dth-order Taylor approximation of the function to be minimized. Add a regularization term to the Taylor approximation, such that the sum is a SOS (sum of squares) convex polynomial. The regularization term can be obtained by solving a semi-definite program. Compute the minimizer of the SOS convex polynomial, which can be done by solving a semi-definite program. Iterate until desired accuracy is achieved.

The paper gives an explicit iteration formula for the univariate case using a 3rd-order Taylor approximation. Consider the function $f(x) = \sqrt(x^2 + 1) - 1$.

| Classical Newton  | Third Order  |
| -------------------------------- |
| Initial point x = 0.9. Iterations: 4. Time: 0.0001 seconds | Initial point x = 0.9. Iterations: 2. Time: 0.007 seconds |
