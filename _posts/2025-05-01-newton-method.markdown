---
layout: post
title:  "Higher-Order Newton Methods"
date:   2025-06-03 12:09:08 -0700
math: true
---

The paper *Higher-Order Newton Methods with Polynomial Work per Iteration* by Ahmadi et al. presents a generalization of Newton's method that uses high-order Taylor approximations of the objective function, in contrast to the quadratic approximation of the classical Newton method. The advantage of using a high-order Taylor approximation is faster local convergance; the paper shows that the d-th order method has local convergence of order d. The basin of convergence is also larger.

The issue with simply extending Newton's method to use high-order Taylor approximations is twofold. First, the problem of minimizing the high-order model, in general, is NP-hard. Second, the the model may not be bounded below - even for an objective that is strongly convex. Take the example given in the paper $f(x) = x^2 - x^4 + x^6$. The fourth order Taylor approximation centered at $x = 0$ is $T(x) = x^2 - x^4$, which is unbounded from below.

The proposed method minimizes a regularized Taylor approximation, $T(x) + t {\lVert x - x_k \rVert}^d$. Here $t$ is the minimum such that the surrogate function is sum-of-squares convex. Finding such a $t$ in polynomial time is possible through solving a semidefinite program. Minimizing the surrogate is also possible through solving a semidefinite program.