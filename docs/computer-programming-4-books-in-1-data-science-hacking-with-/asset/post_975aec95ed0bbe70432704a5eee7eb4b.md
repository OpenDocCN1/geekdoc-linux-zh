
-   Numpy
-   SciPy
-   Matplotlib

For simplicity, you can consider Numpy as your one-stop for arrays. Numpy arrays are different from the typical Python lists in many different ways, but a few to recall is that they are faster, consume less space, and have more functionality. It is important to remember, though, that these arrays are of a fixed size and type, which you define at creation. No infinitely appending new values like you want with a list.

SciPy is defined on top of Numpy and provides a lot of the optimization, linear algebra, and statistics functions you will need. Although sometimes, Numpy has similar functionality, SciPy's functionality is better. If you want to compute a correlation coefficient or generate some normally distributed data, then SciPy is the library for you.

# Matplotlib

This is probably not grabbing any beauty awards, but it is the major library for plotting in Python. It has a lot of functionality and enables you to have huge control when needed.

# 2nd generation

The main libraries are great, and you will find yourself using them a lot. There are three 2nd generation libraries, which have been highly developed on top of the main one to give you additional functionality with less code.

Pandas were designed to make data analysis easier in Python. Pandas make it easy to load structured data, compute statistics on it, and slice and dice the data in whichever way you want. It is one of the most indispensable tools during the data exploration and analysis stage. However, it’s not good to use it in production because it doesn’t scale very well to large datasets. You can gain a huge boost in production by converting your Pandas code to raw Numpy.

Although Matplotlib isn't the best out of the box, Seaborn makes it easy to define beautiful visualizations. It is centered upon Matplotlib, so you can still apply Matplotlib functionality to augment Seaborn charts. It also makes it easier to define complex chart types.

# Chapter 4: Data Manipulation

The Python Pandas library is an open-source project that has easy to use tools for data manipulation and analysis. A significant amount of time in any machine learning project will be required to prepare the data and analyze the basic trends and patterns before creating any models.

The Pandas library has risen into a powerhouse of data manipulation tasks in Python because it was built in 2008. With its elaborate syntax and flexible data structure, it’s easy to learn and support faster data computation. The development of Numpy and Pandas library has stretched Python’s multi-purpose nature to compute machine learning challenges. The acceptance of Python language in machine learning has been critical since then. This is one of the reasons highlighting the need for you to master these libraries.

In the following chapter, you will learn about how to use Numpy and Pandas libraries for data manipulation from scratch. We shall mix both theory and practical aspects.

First, we will recap the syntax and commonly used functions of the respective libraries. Then later work on a real-life data set.

So, you need to be good at the basics of Python. No further knowledge is required. Also, ensure you have Python installed in your machine.

## 6 Key Things You Need to Know About Numpy and Pandas

- The data properties of Pandas are designed on top of the Numpy library. In one way, Numpy is a dependency of the Pandas library.
- Pandas is perfect at handling tabular data sets made of unique variables. Besides that, the Pandas library can still be used to perform even the most naive of tasks such as loading data or performing feature engineering on time series data.
- Numpy is suitable for performing basic numerical computations like median, range, mean, etc. Besides that, it supports the development of multidimensional arrays.
- The Numpy library can also be used to mix C/C++ and Fortran code.
- Keep in mind, Python is a zero-indexing language, unlike R language, where indexing begins at one.
- The best thing about learning Pandas and Numpy is the strong, active community support you gain from the world.

Just to give you a grasp of the Numpy library, we’ll quickly revise its syntax structures and some critical commands such as indexing, slicing, concatenation, etc. All these commands will be useful when using Pandas. Let's get started.

# Getting Started with Numpy

First, load the library and confirm its version, just to be sure that we are not using an older version.

```python
import numpy as np
np.__version__
'1.12.1'
```

Next, build a list of numbers running from 0 to 9.

```python
L = list(range(10))
```

Then convert integers to a string. This method of working with lists is known as a list comprehension.

List comprehension provides a versatile means to deal with list manipulation tasks easily.

# Array Indexing

The important thing to remember is that indexing in Python starts at zero.

```python
x1 = np.array([4, 3, 4, 4, 8, 4])
x1
array([4, 3, 4, 4, 8, 4])
```

```python
#assess value to index zero
x1[0]
4
```

```python
#assess fifth value
x1[4]
8
```

```python
#get the last value
x1[-1]
4
```

```python
#get the second last value
x1[-2]
```

```python
#in a multidimensional array, we need to specify row and column index
x2
array([[[3, 7, 5, 5],
        [0, 1, 5, 9],
        [3, 0, 5, 0]])
```

```python
#1st row and 2nd column value
x2[2,3]
0
```

```python
#3rd row and last value from the 3rd column
x2[2,-1]
0
```

```python
#replace value at 0,0 index
x2[0,0] = 12
x2
array([[12, 7, 5, 5],
        [ 0, 1, 5, 9],
        [ 3, 0, 5, 0]])
```

# Array Slicing

Now, we'll learn to access multiple or a range of elements from an array.

```python
y = np.arange(10)
y
array([0, 1, 2, 3, 4, 5, 6, 7, 8, 9])
```

```python
#from start to 4th position
y[:5]
array([0, 1, 2, 3, 4])
```

```python
#from 4th position to end
y[4:]
```

```python
array([4, 5, 6, 7, 8, 9])
```

```python
#from 4th to 6th position
y[4:7]
array([4, 5, 6])
```

```python
#return elements at even place
y[::2]
array([0, 2, 4, 6, 8])
```

```python
#return elements from first position step by two
y[1::2]
array([1, 3, 5, 7, 9])
```

```python
#reverse the array
y[::-1]
array([9, 8, 7, 6, 5, 4, 3, 2, 1, 0])
```

# Array Concatenation

Many a time, we are required to combine different arrays. So, instead of typing each of their elements manually, you can use array concatenation to handle such tasks easily.

```python
#Using its axis parameter, you can define row-wise or column-wise matrix
np.concatenate([grid,grid],axis=1)
array([[1, 2, 3, 1, 2, 3],
       [4, 5, 6, 4, 5, 6]])
```

Until now, we used the concatenation function of arrays of equal dimension. But, what if you are required to combine a 2D array with a 1D array? In such situations, np.concatenate might not be the best option to use. Instead, you can use np.vstack or np.hstack to do the task. Let’s see how!

```python
x = np.array([3,4,5])
grid = np.array([[1,2,3],[17,18,19]])
np.vstack([x,grid])
array([
    [3, 4, 5],
    [1, 2, 3],
    [17, 18, 19]
])
```

```python
#Similarly, you can add an array using np.hstack
z = np.array([[9],[9]])
np.hstack([grid,z])
array([[ 1, 2, 3, 9],
       [ 4, 5, 6, 9],
       [17, 18, 19, 9]])
```

Besides the functions we have learned above, there are other mathematical functions available in the Numpy library, such as divide, multiple, mod, sin, cos, var, min, max, abs, etc. which you can apply to complete basic arithmetic calculations. Be free to go back to Numpy documentation for additional information on such functions.

Let’s proceed to Pandas now. Ensure you follow every line below because it will enable you to perform the computation using Pandas.

# Getting Started with Pandas

The load library - pd is just an alias. The pd is used because it’s short and literally abbreviates Pandas. Still, you can use any name as an alias.

```python
import pandas as pd
```

Next, create a data frame. Dictionary is used here where keys get converted to column names and values to row values.

```python
data = pd.DataFrame({'Country': ['Russia','Columbia','Chile','Ecuador','Nigeria'],
'Rank':[121,40,100,130,11]})
data
```

| | Country | Rank |
|---|---|---|
| 0 | Russia | 121 |
| 1 | Columbia | 40 |
| 2 | Chile | 100 |
| 3 | Ecuador | 130 |
| 4 | Nigeria | 11 |
