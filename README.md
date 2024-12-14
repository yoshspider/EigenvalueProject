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
  - [Jacobi Method](#Jacobi-Iteration)
  - [Krylov Subspace Method](#Krylov-Subspace-Method)
- [Applications](#Applications)
  - [Differential Equations](#Differential-Equations)
  - [Optimization](#Optimization)
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

Other interesting properties stem for manipulating the matrix $A$.
If $\lambda$ is an eigenvalue for the matrix $A$, $\lambda^k$ is an eigenvalue for the matrix $A^k$. Shifting a matrix $A$ by some $\sigma$ such that $A$ is now $A - \sigma I$, then $\lambda - \sigma$ is an eigenvalue too. Applying any polynomial function to a matrix $A$ would result that such function applied to the eigenvalue would be an eigenvalue of the new matrix. These properties are important to the iterative methodologies of solving for eigenvalues as applying such transformations to matrix to better find eigenvalues can help find the original eigenvalues too.

### Generalized Eigenvalue Problem

The generalized eigenvalue problem is a more complete version of the original eigenvalue problem, which is defined in the following way.

Given square matrices $A$ and $B$, a generalized eigenvector and generalized eigenvalue is defined to be the vector $x$ and $\lambda$ respectively such that it solves the following condition:

$$
\begin{align}
Ax = \lambda Bx \\
\end{align}
$$

This means that the original eigenvalue problem is a subset of the generalized eigenvalue problem such that B is the identity matrix [1].

## Computing Eigenvalues

As discussed before, analytically computing eigenvalues is computationally intensive, and so current methods of solving for eigenvalues utilize iterative methodologies and the properties of eigenvalues before to solve for the eigenvalues.

### Power Iteration

Power Iteration takes advatange of the power rule for eigenvalues in order to solve the eigenvalue problem. The idea is to take with an arbitrary vector $x_0$. The next vector $x_1$ will be defined as $Ax_0$ and for every iteration $i$, $x_i$ will be $Ax_{i-1}$. As the iterations increase, the ratio between $x_i/x_{i-1}$ will approach a corresponding eigenvalue for $x_i$. However, for large iterations, the vector $x_i$ may become either extremely large or small, which can have severe consequences on stability and convergence; therefore, normalization to a unit vector is usually applied to each step. The idea of why this works is that eigenvectors act as these lines of convergence where any vector after each iteration of being multiplied by A, is moving closer and closer to the nearest eigenvector. Power iteration takes advantage of this fact to help find each eigenvector.

The following pseudocode details the process for power iteration.

```
x_previous = rand(n)                                        {Pick a random vector of size n}
x_current = dot(A, x_previous)                              {Find the next iteration value}
ratio = x_current/x_previous                                {Determine initial ratio}
x_current = normalize(x_current)                            {Typically by dividing by ||x_current||}
while (ratio > tolerance):                                  {Continue until the ratio is below a tolerance decided beforehand}
  x_previous = x_current                                    {Repeat iterative process}
  x_current = dot(A, x_previous)
  ratio = x_current/x_previous
  x_current = normalize(x_current)

return x_current, ratio                                     {x_current will be the eigenvector and the ratio will be the eigenvalue}
```

Power Iteration is one of the first numerical methods of finding eigenvalues as serves as a basis for many modern techniques; however, it suffers from multiple problems. One might note that this methodology only returns the most dominant eigenvector (i.e the closest eigenvector) for the randomized initial vector, meaning that smart decisions have to be made about choosing initial vectors such that all eigenvalues are obtained. This also fails in that it can never achieve complex eigenvalues or eigenvectors from the fact that each iteration only has basic operations on real numbers, which can be a cause for concern for more complex applications that require such. Power Iteration also suffers from the fact that it has a slow convergence rate [2].

### QR Iteration

QR Iteration takes advantage of QR factorization which creates an orthonormal basis of vectors to help define the basis of the subspace of A. The idea of why this is helpful is that as opposed to power iteration where one vector is being transformed into the closest eigenvector, an entire subspace can instead be transformed into the eigenspace, returning all the eigenvalues instead of just one at a time. This bypasses the need to have to smartly choose initial vectors and the fact that now one iterative process handles all eigenvalues. Actually, this process of transforming a subspace is called simultaneous iteration and QR iteration is a subset of such.

The iterative process of QR factorization takes the following steps. Take the current matrix A and factor it into Q and R, normalizing to prevent extremely large or small values over time. The next iteration of A will be set as the matrix product of R times Q. Repeat this process until a specified number of iterations or till the matrix A does not significantly change. The diagonal values of the final matrix A will be the eigenvalues and their multiplicities.

This process, while much more expansive than power iteration, is still slow to converge. Therefore, there is a modified algorithm taking advantage of the shift property where matrix A is shifted before each factorization and shifted back afterwards to help the algorithm converge faster [2].

### Jacobi Iteration

Jacobi Iteration is another form of simultaneous iteration except instead of utilzing an orthonormal basis, this method utilizes plane rotations. The idea is that a given subspace can be rotated into the eigenspace by eliminating the non diagonal values, resulting in all the eigenvalues. Jacobi iteration follows the reccurence: $$A_{k+1} = J_k^T A_k J_k $$ where $J_k$ is the $k$ th rotation matrix, which helps delete symmetric elements from the matrix. This methodology has a quadratic rate of convergence and has high accuracy, but can only be utilized on a starting symmetric matrix (for example an undirected graph adjacency matrix) [1].


### Krylov Subspace Method

Kyrlov Subspace Methods are a subset of methods such as Arnoldi Iteration and Lanczos Iteration in which instead of transforming an already existing subspace into the eigenspace, these methods seek to build the eigensubspace one vector at a time. For Arnoldi Iteration, the idea is to take advantage of the Gram Schmidt process which can transform a vector to be orthogonal from a basis of vectors. By iteraively applying the $A^k b$ vector to be orthogalinized from all previous vectors, this can create an orthogonal basis for the eigenspace, helping find the eigenvalues. This works by a similar idea of power iteration as by orthogonalizing the next vector, it must be closer to a different eigenvalue (unless it has a higher multiplicity than 1). Lanczos Iteration goes a step further for symmetric matrices by first turning them to become tridiagonal, and then applying such an iterative method as this is computationally much faster [2].

## Applications

### Differential Equations

Eigenvalue computation has important applications in differential equations. Both n-order ordinary differential equations and partial differential equations can be converted into matrix form such that the eigenvalues of such a matrix will be the solution set for the set of differential equations. For example, a second order differential equation such as $$y'' + 4y' + 3y = 0$$ (which can represent a wide variety of physics problems such as a spring-mass problem) can be transformed into a matrix problem where a vector $x$ represents $[y, y']$ and the equality $x' = Ax$ can be setup where $A$ would be the coefficients to make this equation true. This looks very similar to the definition of an eigenvector, and the solution set would just be the sum of each eigenvector times $e^\lambda$ pair. Both complex and generalized eigenvalues result in real solutions for less trivial differential equations. 

More complex differential equations can be mapped to the generalized eigenvalue problem of $$Dv' + Cv = 0$$ whose solution set solves the differential equation. An example use of such is finding solutions for the Brusselator model, which is a set of differential equations to model chemical reactions in a reactor. These results help transform a series of differential equations which analytically would require a complex ruleset of different methodologies to the generalized eigenvalue problem which can straightfowardly solved for its eigenvalues and thereby its solution set through one of the previously listed methodologies [3].

### Optimization

Eigenvalues have significant applications when it comes to linear programming and optimization, which has a wide variety of applications throughout all fields. One of the earliest instances of such is NP-hard Optimal Partioning of Graphs problem which seeks to take an undirected graph and to optimally split it such that each subset has the exactly same number of vertices and that the edges between subsets is minimized. Interestingly, by utilzing an adjacency matrix as a representation of such graph, Donath and Hoffman were able to turn it into an optimization problem by creating a new matrix representation to show which vertex is part of which subset. With some more analytical research, they were able to find that this optimization can be done through eigenvalues. In fact many graph problems such as max cut can be transformed into eigenvalue optimization problems which can be strong approximations for known NP-hard problems [4].

### Eigenvalues for Numerical Methods

## References
1. Heath, M. T. (2009). Chapter 4: Eigenvalue Problems. In Scientific computing: An introductory survey (pp. 157–214), McGraw Hill.
2. Golub, G. H., & van der Vorst, H. A. (2000). Eigenvalue computation in the 20th century. Journal of Computational and Applied Mathematics, 123(1–2), 35–65. https://doi.org/10.1016/s0377-0427(00)00413-1
3. HarrarII, D. L., & Osborne, M. R. (2003). Computing eigenvalues of ordinary differential equations. ANZIAM Journal, 44, 313. https://doi.org/10.21914/anziamj.v44i0.684  
4. Lewis, A. S., & Overton, M. L. (1996). Eigenvalue optimization. Acta Numerica, 5, 149–190. https://doi.org/10.1017/S0962492900002646
5. 
