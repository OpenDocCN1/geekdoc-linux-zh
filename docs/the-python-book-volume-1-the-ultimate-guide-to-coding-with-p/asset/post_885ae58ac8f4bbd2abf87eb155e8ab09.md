
![](img/3b256f430f51c98f1315671f6e4eec19_85_0.png)

## Work with Python

## 09 Plotting with Matplotlib

09 Plotting with Matplotlib
The first move you should make is to install Matplotlib. As you can see, Matplotlib has many dependencies that you should also install.
The first thing you will learn is how to plot a polynomial function. The necessary commands for plotting the 3x^2-x+1 polynomial are the following:

```
import numpy as np
import matplotlib.pyplot as plt
myPoly = np.poly1d(np.array([3, -1, 1]))
astype(float)
x = np.linspace(-5, 5, 100)
y = myPoly(x)
plt.xlabel('x values')
plt.ylabel('f(x) values')
xticks = np.arange(-5, 5, 10)
yticks = np.arange(0, 100, 10)
plt.xticks(xticks)
plt.yticks(yticks)
plt.grid(True)
plt.plot(x,y)
```

The variable that holds the polynomial is myPoly. The range of values that will be plotted for x is defined using "x = np.linspace(-5, 5, 100)". The other important variable is y, which calculates and holds the values of f(x) for each x value.
It is important that you start ipython using the "--pylab=qt" parameters in order to see the output on your screen. If you are interested in plotting polynomial functions, you should experiment more, as NumPy can also calculate the derivatives of a function and plot multiple functions in the same output.

> SciPy is built on top of NumPy and is more advanced

```
In [36]: from scipy.stats import poisson, lognorm
In [37]: mySh = 10;
In [38]: myMu = 10;
In [39]: ln = lognorm(mySh)
In [40]: p = poisson(myMu)
In [41]: ln.rvs(10e6)
Out[41]:
array([[ 9.2939114e-02, 1.15957068e+01, 9.70411903e+01,
        8.26370734e-07, 5.64451441e-03, 4.61744655e-09,
        4.98471222e-06, 1.45947948e+02, 9.25502852e-06,
        5.8753728e-02]])
In [42]: p.rvs(10)
Out[42]: array([12, 11, 9, 9, 9, 10, 9, 4, 13, 8])
In [43]: ln.pdf(3)
Out[43]: 0.013218867177522842
```

## 10 About SciPy

SciPy is built on top of NumPy and is more advanced than NumPy. It supports numerical integration, optimisations, signal processing, image and audio processing, and statistics. The example in Fig. 01 (to the left) uses a small part of the scipy.stats package that is about statistics.
The example uses two statistics distributions and may be difficult to understand even if you know mathematics, but it is presented in order to give you a better taste of SciPy commands.

## 11 Using SciPy for image processing

Now we will show you how to process and transform a PNG image using SciPy.
The most important part of the code is the following line:

```
image = np.array(Image.open('SA.png').convert('L'))
```

This line allows you to read a usual PNG file and convert it into a NumPy array for additional processing. The program will also separate the output into four parts and displays a different image for each of these four parts.

## 12 Other useful functions

It is very useful to be able to find out the data type of the elements in an array; it can be done using the dtype() function. Similarly, the ndim() function returns the number of dimensions of an array. When reading data from external files, you can save their data columns into separate variables using the following way:

```
In [10]: a1,a2 = np.loadtxt("timeN.txt", usecols=(0,1), unpack=True)
```

The aforementioned command saves column 1 into variable aa1 and column 2 into variable aa2. The "unpack=True" allows the data to be assigned to two different variables. Please note that the numbering of columns starts with 0.

## 13 Fitting to polynomials

The NumPy polyfit() function tries to fit a set of data points to a polynomial. The data was found from the timeN.txt file, created earlier in this article.

The Python script uses a fifth degree polynomial, but if you want to use a different degree instead then you only have to change the following line:

```
coefficients = np.polyfit(aa1, aa2, 5)
```

## 14 Array broadcasting in NumPy

To close, we will talk more about array broadcasting because it is a very useful characteristic. First, you should know that array broadcasting has a rule: in order for two arrays to be considered for array broadcasting, "the size of the trailing axes for both arrays in an operation must either be the same size or one of them must be one." Put simply, array broadcasting allows NumPy to "change" the dimensions of an array by filling it with data in order to be able to do calculations with another array. Nevertheless, you cannot stretch both dimensions of an array to do your job.

Process and transform a PNG image using SciPy

![](img/3b256f430f51c98f1315671f6e4eec19_86_0.png)

![](img/3b256f430f51c98f1315671f6e4eec19_86_1.png)
