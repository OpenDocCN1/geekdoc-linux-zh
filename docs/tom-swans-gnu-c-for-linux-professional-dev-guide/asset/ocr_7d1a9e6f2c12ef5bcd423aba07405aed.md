> Note
> In some versions of C++, cols is required to be a constant; only rows may be variable. However, GNU C++ permits variables in creating arrays of any dimensions.

The expression matrix[r][c] refers to a single element in the matrix at row r and column c. For fun, the sample program uses this expression to fill the matrix with some values, and then writes them to the standard output in column order. Onscreen, you see something like this:

```
$ g++ newmatrix.cpp
$ ./a.out
Rows (1 ... 9) ? 3
Columns (1 ... 10) ? 4
  1   2   3
  2   4   6
  3   6   9
  4   8  12
```

More than two dimensions are rarely useful, but C++ places no restriction on the depth of a multidimensional array. To create an 8-by-8-by-8 cube, you could use these statements:

```
int (* matrix)[8][8];
matrix = new int[8][8][8];
```

Again, in the first line, you are merely declaring matrix as a pointer that potentially addresses a multidimensional array. As declared here, matrix is literally a pointer (an array) of 8 arrays of 8 arrays—conceptually, a three-dimensional cube. It's possible to carry this idea to extremes, adding additional dimensions, but is there a practical use for a four- or higher-dimensional matrix? If there is, I've never seen it!

# PASSING ARGUMENTS TO main()

Using pointers, you can access arguments passed to main(). This is an essential technique for obtaining command-line options, filenames, and other data entered by users when they run the program. Listing 11.4, cmdline.cpp, shows one way to pick up command-line arguments.

# LISTING 11.4 CMDLINE.CPP

```
#include <iostream.h>

int main(int argc, char *argv[])
{
    cout << "Command line arguments:" << endl;
    for (int i = 1; i < argc; i++)
        cout << argv[i] << endl;
    return 0;
}
```