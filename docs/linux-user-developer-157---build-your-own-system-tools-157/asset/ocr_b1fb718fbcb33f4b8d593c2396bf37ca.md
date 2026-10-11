```
> aDataFrame = data.frame(v1=c(1,2,3,4,5), v2=c(0,1,2,3,4), v3=c(-1,-2,-3,-4,-5), v4=c(0,0,1,2,3), v5=c(-1,-2,-3,-4,-5))
> aDataFrame
  v1 v2 v3 v4 v5
1  1 0 -1  0 -1
2  2 1 -2  0 -2
3  3 2 -3  1 -3
4  4 3 -4  2 -4
5  5 4 -5  3 -5
> aDataFrame[4,3]
[1] -4
> aDataFrame[4,3] = aDataFrame[4,3] + 100
> aDataFrame
  v1 v2 v3 v4 v5
1  1 0 -1  0 -1
2  2 1 -2  0 -2
3  3 2 -3  1 -3
4  4 3 96  2 -4
5  5 4 -5  3 -5
> aDataFrame[,1]
```

Left R enables you to apply operations to specific rows and columns of a table

```
> myDataFrame$v1 - 5
[1] -4 -3 -2 -1  0
```

```
> anotherMatrix <- matrix(unlist(myList), ncol = 2, byrow = TRUE)
```

# Get help

The following command adds ten to all elements of the first row:

The previous command requires that you manually specify the number of columns of the new matrix because you are converting a linear type into a two-dimensional one. You can transform a vector named aVector into a list as follows:

R offers a plethora of ways to get help about functions: if you type a question mark at the R prompt, followed by the name of a function, R will return something similar to Unix man pages:

```
> myDataFrame[, ] + 10
```

```
> anotherList <- as.list(aVector)
```

```
? Sys.sleep
```

The following command adds minus one to the first column, zero to the second and one to the third column of myDataFrame:

You can convert a list named anotherList into a vector with the help of the unlist() function:

```
The following command will return working examples for the read.table() function:
```

```
> myDataFrame + -1:1
```

```
> aNewVector <- unlist(anotherList)
```

```
? example(read.table)
```

Remember that as long as you do not assign the result of an operation to the myDataFrame variable, the original contents of myDataFrame will not change.

The next command creates a new column named sum to myDataFrame that contains the sum of all values of each row:

# 10  Save and load your work

```
The next command will show you an impressive demo of the graphic capabilities of R:
```

```
> myDataFrame$sum = myDataFrame$v1 + 
myDataFrame$v2 + myDataFrame$v3
```

So far, you have seen how to change your data in various ways. The final step will describe how to save your data and load it the next time you run R. You can save your current R session, including all defined variables, as follows:

```
capabilities()
```

As you can understand, this operation does alter myDataFrame by adding a new column to it. Using the same method, you can perform any kind of calculations you want.

```
> save(list = ls(all=TRUE), file = "R25Aug2015")
```

The next commands will show you an impressive demo of the graphic capabilities of R:

# 09  Convert between various data types

```
R25Aug2015.capabilities()
```

This step will show you how to convert between lists, data frames, vectors and matrices. Given a matrix named myMatrix, you can convert it into a list using the following command:

The operating system will create a file named R25Aug2015 that you can load afterwards as follows:

```
> load((file = "R25Aug2015")
```

```
> myList <- as.list(data.frame(t(myMatrix)))
```

The following command can be used for removing all currently defined types of R objects:

```
> rm(list=ls())
```

Given a list name myList, you can convert it into a matrix with this command:

R is an endless subject and you can only learn more about it by practising, so start experimenting and give your data many new meanings!