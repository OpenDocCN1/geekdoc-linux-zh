![](bbox=[0.13, 0.12, 0.89, 0.55])

*Figure 5. How to Obtain an N Value from an Error Message and in Your Program*

# Here Is an Example of What Happens When You Use These Two Techniques

The following example illustrates all the actions taken by the ESSL error-handling facility for each possible value of a recoverable input argument, *n*. The values of *n* used in the example are as follows:

| N | Meaning of the N Value |
| :--- | :--- |
| 7208960 | An acceptable transform length, required for successful computing of a Fourier transform |
| 7340032 | The next larger acceptable transform length, required for successful computing of a Fourier transform |

Table 28 on page 42 describes the actions taken by ESSL in every possible situation for the values given in this example.