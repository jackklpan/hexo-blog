---
title: Linear Algebra
tags: []
date: 2014-12-18 00:23:00
---

\( 2x-y = 0 \) 
\( -x+2y = 3 \) 
Row picture: intersection of planes 
\( \begin{bmatrix}  2 & -1 \\ -1 & 2 \end{bmatrix} \begin{bmatrix} x \\ y \end{bmatrix} =  \begin{bmatrix} 0 \\ 3 \end{bmatrix} \) 
Column picture: combine vectors to produce right hand. Or called it as a linear combination of columns.
\(  x \begin{bmatrix} 2 \\ -1      \end{bmatrix} +  y \begin{bmatrix} -1 \\ 2 \end{bmatrix}  = \begin{bmatrix} 0 \\ 3 \end{bmatrix} \) 
Ax = b have solution when A is invertible(non-singular case). 
And we can say Ax is a combination of columns of A. 

# Elimination
Select the first row first column as pivot, and elimination all row below it, to make these row's first columns become zero. 
Then select the second row second column as pivot. elimination all row below it to make these row's second columns become zero. 
Do it recursive until reach the last row. 

**One thing to note is "pivots cannot be zero"** 

So the elimination fail when A matrix is singular matrix. 
We can exchange the row's positions to make pivots not zero when A matrix is not singular matrix. 
\( \begin{bmatrix} 0 & 1 \\ 1 & 0 \end{bmatrix} \begin{bmatrix} 0 & 2 \\ 3 & 1 \end{bmatrix} = \begin{bmatrix} 3 & 1 \\ 0 & 2 \end{bmatrix} \) 
And we can express these operations in matrix form. 
(When we put a matrix in the left of A, it is a combination of **rows** of A. Just like the above example to exchange row 1 and row 2\. 
 When we put a matrix in the right of A, it is a combination of **columns** of A. Like the below example to exchange col 1 and col 2.) 
\( \begin{bmatrix} 0 & 2 & 1\\ 3 & 1 & 2\\ 1 & 2 & 3 \end{bmatrix} \begin{bmatrix} 0 & 1 & 0 \\ 1 & 0 & 0 \\ 0 & 0 & 1 \end{bmatrix}  = \begin{bmatrix} 2 & 0 & 1 \\ 1 & 3 & 2 \\ 2 & 1 & 3 \end{bmatrix} \) 

Example for elimination: 
\( x+2y+z = 2 \) 
\( 3x+8y+z = 12 \) 
\(  4y+z = 2 \) 
\( \begin{bmatrix} 1 & 0 & 0 \\ 0 & 1 & 0 \\ 0 & -2 & 1 \end{bmatrix} \begin{bmatrix} 1 & 0 & 0 \\ -3 & 1 & 0 \\ 0 & 0 & 1 \end{bmatrix} \begin{bmatrix} 1 & 2 & 1 \\ 3 & 8 & 1 \\ 0 & 4 & 1 \end{bmatrix} =  \begin{bmatrix} 1 & 2 & 1 \\ 0 & 2 & -2 \\ 0 & 0 & 5 \end{bmatrix} \) 
It can be expressed as: 
\( E_{32} E_{21} A = U \) or just \( E A = U \) 
So do the same multiplication on b, we can get z value first. And back-substitution to get x and y. 

# Multiplication
Not commutative, but associative. 
\( AB = C \) 
\( A=m*n \qquad B=n*p \qquad C=m*p \) 

1.  Row times column\( C_{34} = (row\,3\,of\,A) \cdot (column\,4\,of\,B) = a_{31}b_{14} + a_{32}b_{24} + ... = \sum\limits_{k=1}^n a_{3k}b_{k4} \)2.  Column wayColumns of C are combinations of columns of A\( \begin{bmatrix} \; & \; \end{bmatrix} \begin{bmatrix} | & | \end{bmatrix} = \begin{bmatrix} | & | \end{bmatrix} \)3.  Row wayRows of C are combinations of rows of B\( \begin{bmatrix} - \end{bmatrix} \begin{bmatrix} \; \end{bmatrix} = \begin{bmatrix} - \end{bmatrix} \)4.  Column times rowSum of (cols of A) * (rows of B)\( \begin{bmatrix} 2 & 7 \\ 3 & 8 \\ 4 & 9 \end{bmatrix} \begin{bmatrix} 1 & 6 \\ 0 & 0 \end{bmatrix} = \begin{bmatrix} 2 \\ 3 \\ 4 \end{bmatrix} \begin{bmatrix} 1 & 6 \end{bmatrix} + \begin{bmatrix} 7 \\ 8 \\ 9 \end{bmatrix} \begin{bmatrix} 0 & 0 \end{bmatrix} \)5.  Block way\( \begin{bmatrix} A_1 & A_2 \\ A_3 & A_4 \end{bmatrix} \begin{bmatrix} B_1 & B_2 \\ B_3 & B_4 \end{bmatrix} = \begin{bmatrix} A_1B_1+A_2B_3 & \_ \\ \_ & \_ \end{bmatrix} \)

# Inverses of square matrices
\( A^{-1}A = I = AA^{-1} \) 
Only when matrix is square, we can put inverse of A after A to get I. (A must to be square to be invertible?)
But **not all matrices have inverses. An inverse is <span style="color:red">impossible</span> when Ax is zero and x is non zero.** 
Because \( A^{-1}Ax = A^{-1}0 \) means \( Ix = A^{-1}0 \) means \( x = 0 \). So it is impossible to find inverse of A when x is nonzero and there exist Ax is zero. 
**The inverse exists if and only if elimination produces n pivots** 

**Gauss-Jordan method to compute inverse of A** 
Put the matrix in the form \( \begin{bmatrix} A & I \end{bmatrix} \) and start the elimination to make A become triangular U. And then do it backward to make U become I. 
The matrix become \( \begin{bmatrix} I & ? \end{bmatrix} \). 
Actually ? is \( A^{-1} \). 
If we let E matrix is the steps we do in A to let A become I, we know that \( E \begin{bmatrix} A & I \end{bmatrix} =  \begin{bmatrix} I & ? \end{bmatrix} \). 
So \( EA = I \) => \( E = A^{-1} \), means \( EI = A^{-1} \). Therefore the ? in the right is what we want \( A^{-1} \).