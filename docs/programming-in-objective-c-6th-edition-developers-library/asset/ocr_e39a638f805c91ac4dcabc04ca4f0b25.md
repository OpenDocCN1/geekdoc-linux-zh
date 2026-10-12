```
return 0;
}

// Function to multiply a matrix by a scalar

void scalarMultiply (int nRows, int nCols,
                    int matrix[nRows][nCols], int  scalar)
{
  int  row, column;

  for (  row = 0;  row < nRows;  ++row )
    for (  column = 0;  column < nCols;  ++column )
      matrix[row][column]  *=  scalar;
}

void  displayMatrix (int nRows, int nCols, int  matrix[nRows][nCols])
{
  int  row, column;

  for (  row = 0;  row < nRows;  ++row) {
    for (  column = 0;  column < nCols;  ++column )
      printf ("%5i",  matrix[row][column]);

    printf ("\n");
  }
}
```