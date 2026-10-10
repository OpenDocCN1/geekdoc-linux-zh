the upper left triangle of the array, but may not occur in the lower right triangle of the array, as you can see from the examples given here.

Following is an example where $m > n$, and general band matrix $A$ is 9 by 8 with band widths of $ml = 2$ and $mu = 3$.

Given the following matrix $A$: \[
\begin{bmatrix}
11 & 12 & 13 & 14 & 0 & 0 & 0 & 0 \n21 & 22 & 23 & 24 & 25 & 0 & 0 & 0 \n31 & 32 & 33 & 34 & 35 & 36 & 0 & 0 \n0 & 42 & 43 & 44 & 45 & 46 & 47 & 0 \n0 & 0 & 53 & 54 & 55 & 56 & 57 & 58 \n0 & 0 & 0 & 64 & 65 & 66 & 67 & 68 \n0 & 0 & 0 & 0 & 75 & 76 & 77 & 78 \n0 & 0 & 0 & 0 & 0 & 86 & 87 & 88 \n0 & 0 & 0 & 0 & 0 & 0 & 97 & 98
\end{bmatrix}
\]

you store it in array $\texttt{AGB}$, declared as $\texttt{AGB}(6,8)$, as follows, where $a_{11}$ is stored in $\texttt{AGB}(4,1)$:

$$\texttt{AGB} = \begin{bmatrix}
* & * & * & 14 & 25 & 36 & 47 & 58 \n* & * & 13 & 24 & 35 & 46 & 57 & 68 \n* & 12 & 23 & 34 & 45 & 56 & 67 & 78 \n11 & 22 & 33 & 44 & 55 & 66 & 77 & 88 \n21 & 32 & 43 & 54 & 65 & 76 & 87 & 98 \n31 & 42 & 53 & 64 & 75 & 86 & 97 & *
\end{bmatrix}$$

Following is an example where $m < n$, and general band matrix $A$ is 7 by 9 with band widths of $ml = 2$ and $mu = 3$.

Given the following matrix $A$: \[
\begin{bmatrix}
11 & 12 & 13 & 14 & 0 & 0 & 0 & 0 & 0 \n21 & 22 & 23 & 24 & 25 & 0 & 0 & 0 & 0 \n31 & 32 & 33 & 34 & 35 & 36 & 0 & 0 & 0 \n0 & 42 & 43 & 44 & 45 & 46 & 47 & 0 & 0 \n0 & 0 & 53 & 54 & 55 & 56 & 57 & 58 & 0 \n0 & 0 & 0 & 64 & 65 & 66 & 67 & 68 & 69 \n0 & 0 & 0 & 0 & 75 & 76 & 77 & 78 & 79
\end{bmatrix}
\]

you store it in array $\texttt{AGB}$, declared as $\texttt{AGB}(6,9)$, as follows, where $a_{11}$ is stored in $\texttt{AGB}(4,1)$ and the leading diagonal does not fill up the whole row:

$$\texttt{AGB} = \begin{bmatrix}
* & * & * & 14 & 25 & 36 & 47 & 58 & 69 \n* & * & 13 & 24 & 35 & 46 & 57 & 68 & 79 \n* & 12 & 23 & 34 & 45 & 56 & 67 & 78 & * \n11 & 22 & 33 & 44 & 55 & 66 & 77 & * & * \n21 & 32 & 43 & 54 & 65 & 76 & * & * & * \n31 & 42 & 53 & 64 & 75 & * & * & * & *
\end{bmatrix}$$

and where `"*"` means you do not store an element in that position in the array.

Following is an example of how to transform your general band matrix, for all values of $m$ and $n$, to BLAS5-general-band storage mode: