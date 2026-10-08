# Scientific computing with NumPy

# Work with Python

![](bbox=[0.106, 0.105, 0.943, 0.638])

```
np.loadtxt("timeN.txt", usecols=(0,1), unpack=True)
```

The aforementioned command saves column 1 into variable aa1, column 2 into aa2. The "Unpack=True" allows the data to be assigned to two different variables. Please note that the number of columns starts with 0.

The Python script uses a fifth polynomial, but if you want to use a different degree instead then you have to change the following line:

should know that array broadcasting has a rule in order for two arrays to be considered for array broadcasting, "the size of the trailing axes for both arrays in an operation must either be the same-size or one of them must be."

+   - coefficients = np.polyfit(aa1, aa2, 5)

Put simply, array broadcasting allows NumPy to "change" the dimensions of an array by filling it with data to be able calculations with another array. Nevertheless, you cannot stretch both dimensions of an array to do your job.

# Fitting to polynomials

+   13 NumPy polyfit() function tries to fit a set of data points to a polynomial. The data was found in the timeN.txt file, created earlier

# Array broadcasting in NumPy

+   14 To close, we will talk more about array broadcasting because it is a very useful characteristic. First, you

+   * Next