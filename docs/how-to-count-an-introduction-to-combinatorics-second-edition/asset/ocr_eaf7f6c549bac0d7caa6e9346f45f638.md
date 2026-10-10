polynomial of degree 2 we try to find a particular solution of the same form, that is, with \( a_n = \alpha n^2 + \beta n + \gamma \). Substituting this into the recurrence relation gives

$$(\alpha n^2 + \beta n + \gamma) - 5(\alpha(n - 1)^2 + \beta(n - 1) + \gamma) + 6(\alpha(n - 2)^2 + \beta(n - 2) + \gamma) = n^2 \ .$$

That is,

$$2\alpha n^2 + (-14\alpha + 2\beta) n + (19\alpha - 7\beta + 2\gamma) = 2n^2 .$$

Equating the coefficients of \( n^2 \) and \( n \) and the constant terms gives \( 2\alpha = 2 \), \( -14\alpha + 2\beta = 0 \), and \( 19\alpha - 7\beta + 2\gamma = 0 \). Hence \( \alpha = 1 \), \( \beta = 7 \), and \( \gamma = 15 \). Therefore, the general solution of the nonhomogeneous recurrence relation is given by

$$a_n = A 2^n + B 3^n + n^2 + 7 n + 15 .$$

The initial conditions give \( 2A + 3B + 23 = 28 \) and \( 4A + 9B + 33 = 34 \), that is, \( 2A + 3B = 5 \) and \( 4A + 9B = 1 \). Hence \( A = 7 \) and \( B = -3 \). Therefore the solution is

$$a_n = 7(2^n) - 3(3^n) + n^2 + 7n + 15 .$$

# ### Exercises

+   - **7.6.1A** Find a formula for \( a_n \) given that \( a_n - 2a_{n-1} - 8a_{n-2} = 18 - 9n \), with \( a_1 = 1 \) and \( a_2 = 3 \).

+   - **7.6.1B** Find a formula for \( a_n \) given that \( a_n + 5a_{n-1} + 6a_{n-2} = 2n^2 - 21n^2 + 57n - 43 \) for \( n \geq 3 \) with \( a_1 = 1 \) and \( a_2 = 14 \).

+   - **7.6.2A** Let \( a_n \) be the number of sequences of length \( n \) of letters of the English alphabet in which between them the five vowels, A, E, I, O, U, occur an even number of times.
+   					- i. Show that \( a_1 = 21 \) and that, for \( n \geq 2 \), \( a_n = 16a_{n-1} + 5(26^{n-1}) \).
+   					- ii. Find a formula for \( a_n \).

+   - **7.6.2B** Let \( a_n \) be the number of \( n \)-digit sequences formed using only the digits 0, 1, 2, and 3 in which 0 occurs an odd number of times.
+   					- i. Show that \( a_n = 2a_{n-1} + 4^{n-1} \).
+   					- ii. Find a formula for \( a_n \).

+   - **7.6.3A** Let \( m \) and \( n \) be positive integers with \( m < n \). How many arithmetic operations are needed to row-reduce an \( m \times n \) matrix to echelon form?

+   - **7.6.3B** Let \( \mathbf{A} \) be an invertible (that is, nonsingular) \( n \times n \) matrix. The inverse of \( \mathbf{A} \) may be calculated by forming the \( n \times 2n \) matrix \( (\mathbf{A} \vert \mathbf{I}_n) \) by writing the \( n \times n \) identity matrix \( \mathbf{I}_n \) alongside \( \mathbf{A} \) and then row-reducing this matrix to echelon form, thus obtaining a matrix of the form \( (\mathbf{I}_n \vert \mathbf{B}) \), where \( \mathbf{B} \) is the inverse of \( \mathbf{A} \). How many arithmetic operations are needed to calculate the inverse of \( \mathbf{A} \) by this method?

+   - **7.6.4A** \(\textit{The Tower of Hanoi}\)
+   					Suppose that we have three pegs. On one of these pegs there are \( n \) disks of different sizes arranged in order of size with the largest disk at the bottom. The task is to transfer these \( n \) disks to the third peg, by moving one disk at