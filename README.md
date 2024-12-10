---
Name: Yash Agrawal
Topic: Eigenvalues and Generalized Eigenvalues
Title: The Eigenvalue Problem and its Applications
---
# The Eigenvalue Problem and its Applications
## Table of Contents
- [Overview](#Overview)
- [Background](#Background)
  - Generalized Eigenvalue Problem
- Computing Eigenvalues
  - Power Iteration
  - Inverse Iteration
  - QR Iteration
  - Jacobi Method
  - Relatively Robust Representation
- Applications
  - Differential Equations
  - Graph Theory
  - Principal Component Analysis
 - Eigenvalues Value in Numerical Methods



## Overview

Given a square matrix $A$, an eigenvector and eigenvalue is defined to be the vector $x$ and $\lambda$ respectively such that it solves the following condition:

$$
\begin{align}
Ax = \lambda x \\
\end{align}
$$

Therefore, the eigenvalue problem is to find the set of all eigenvalues (also known as the spectrum of a matrix) and the set of all eigenvectors (whose basis create a vector subspace that is known as the eigenspace of a matrix) of a given matrix. Eigenvalues contain numerous different properties with a wide variety of applications, many of which will be discussed here, and so solving the eigenvalue problem (within reasonable precision) is a critical task in science, mathematics, and engineering.

## Background

To solve for eigenvalues and eigenvectors analytically, the go to method is solving the characteristic polynomial which is achieved to rearranging the definition in the following way where I is the identity matrix of the same size of A:

$$
\begin{align}
Ax = \lambda x \\
Ax - \lambda x = 0 \\
(A - \lambda \ I) \ x = 0 \\
\end{align}
$$

Therefore, solving $det(A - I \lambda) = 0$ will result in all the eigenvalues and eigenvectors of matrix A. Note that if matrix A has $n$ x $n$ dimensions, solving this characteristic polynomial will result in max $n$ solutions, meaning that the number of eigenvalues for a matrix is bounded by $rank(A)$.


