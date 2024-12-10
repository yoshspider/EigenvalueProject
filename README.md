---
Name: Yash Agrawal
Topic: Eigenvalues and Generalized Eigenvalues
Title: The Eigenvalue Problem and its Applications
---
# The Eigenvalue Problem and its Applications
## Table of Contents
- [Overview](#Overview)
- [Background](#Background)
  - [Generalized Eigenvalue Problem](#Generalized-Eigenvalue-Problem)
- [Computing Eigenvalues](#Computing-Eigenvalues)
  - [Power Iteration](#Power-Iteration)
  - [QR Iteration](#QR-Iteration)
  - [Jacobi Method](#Jacobi-Method)
  - [Relatively Robust Representation](#Relatively-Robust-Representation)
- [Applications](#Applications)
  - [Differential Equations](#Differential-Equations)
  - [Graph Theory](#Graph-Theory)
  - [Eigenvalues for Numerical Methods](#Eigenvalues-for-Numerical-Methods)



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

Therefore, solving $det(A - I \lambda) = 0$ will result in all the eigenvalues and eigenvectors of matrix A. Note that if matrix A has $n$ x $n$ dimensions, solving this characteristic polynomial will result in max $n$ solutions, meaning that the number of eigenvalues for a matrix is bounded by $rank(A)$ However, finding the determinant of a matrix, let alone solving such is computationally intensive for large matrixes, and so the eigenvalues is typically estimated through numerical methods.

Two interesting properties as a result of characteristic polynomial is that the sum of the set of eigenvalues is equilivant to the $trace(A)$ and that if $a+bi$ is an eigenvalue of matrix A, then $a-bi$ must be also.

### Generalized Eigenvalue Problem

The generalized eigenvalue problem is a more complete version of the original eigenvalue problem, which is defined in the following way.

Given square matrices $A$ and $B$, a generalized eigenvector and generalized eigenvalue is defined to be the vector $x$ and $\lambda$ respectively such that it solves the following condition:

$$
\begin{align}
Ax = \lambda Bx \\
\end{align}
$$

This means that the original eigenvalue problem is a subset of the generalized eigenvalue problem such that B is the identity matrix.

## Computing Eigenvalues

As discussed before, analytically computing eigenvalues is computationally intensive, and so current methods of solving for eigenvalues utilize iterative methodologies and the properties of eigenvalues before to solve for the eigenvalues.

### Power Iteration

Power Iteration takes advatange of the power rule for eigenvalues in order to solve the eigenvalue problem. The idea is to take with an arbitrary vector $x_0$. The next vector $x_1$ will be defined as $Ax_0$ and for every iteration $i$, $x_i$ will be $Ax_i-1$.

### QR Iteration

### Jacobi Iteration

### Relatively Robust Representation

## Applications

### Differential Equations

### Graph Theory

### Eigenvalues for Numerical Methods
