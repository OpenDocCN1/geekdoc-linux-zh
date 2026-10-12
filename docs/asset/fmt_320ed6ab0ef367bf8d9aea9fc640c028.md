
```c
// Function to find the minimum value in an array

#include <stdio.h>

int  minimum (int  values[], int  numberOfElements)
{
    int  minValue, i;

    minValue = values[0];

    for (  i = 1;  i < numberOfElements;  ++i  )
        if (  values[i] < minValue  )
             minValue = values[i];

    return minValue;
}

int main (void)
{
    int  array1[5] = {  157, -28, -37,  26,  10  };
    int  array2[7] = {  12,  45,  1, 10,  5,  3, 22  };
    int  minimum (int  values[], int  numberOfElements);

    printf ("array1 minimum: %i\n", minimum (array1, 5));
    printf ("array2 minimum: %i\n", minimum (array2, 7));

    return 0;
}
```

```c
#include <stdio.h>

void  multiplyBy2 (float  array[], int  n)
{
    int   i;

    for ( i = 0;  i < n;  ++i )
        array[i] *= 2;
}

int main (void)
{

    float  floatVals[4] = { 1.2f, -3.7f, 6.2f, 8.55f };
    int      i;
    void  multiplyBy2 (float  array[], int  n);

    multiplyBy2 (floatVals, 4);

    for ( i = 0;  i < 4;  ++i )
        printf ("%.2f   ", floatVals[i]);

    printf ("\n");

    return 0;
}
```

```c
// Program to sort an array of integers into ascending order

#include <stdio.h>

void sort(int a[], int n)
{
	int i, j, temp;

	for(i = 0; i < n - 1; ++i)
		for(j = i + 1; j < n; ++j)
			if (a[i] > a[j]) {
				temp = a[i];
				a[i] = a[j];
				a[j] = temp;
			}
}

int main(void)
{
	int i;
	int array[16] = { 34, -5, 6, 0, 12, 100, 56, 22,
				44, -3, -9, 12, 17, 22, 6, 11 };
	void sort(int a[], int n);

	printf("The array before the sort:\n");

	for(i = 0; i < 16; ++i)
		printf("%i ", array[i]);

	sort(array, 16);

	printf("\n\nThe array after the sort:\n");

	for(i = 0; i < 16; ++i)
		printf("%i ", array[i]);

	printf("\n");

	return 0;
}
```

排序前的数组：

`34 -5 6 0 12 100 56 22 44 -3 -9 12 17 22 6 11`

排序后的数组：

`-9 -5 -3 0 6 6 11 12 12 12 17 22 22 34 44 56 100`

```c
scalarMultiply (measured_values, constant);
```

```c
int array_values[100][50]
```

```c
#include <stdio.h>

int main (void)
{
    void scalarMultiply (int matrix[3][5], int scalar);
    void displayMatrix (int matrix[3][5]);
    int sampleMatrix[3][5] =
    {
        { 7, 16, 55, 13, 12 },
        { 12, 10, 52, 0, 7 },
        { -2, 1, 2, 4, 9 }
    };

    printf ("Original matrix:\n");
    displayMatrix (sampleMatrix);

    scalarMultiply (sampleMatrix, 2);

    printf ("\nMultiplied by 2:\n");
    displayMatrix (sampleMatrix);

    scalarMultiply (sampleMatrix, -1);

    printf ("\nThen multiplied by -1:\n");
    displayMatrix (sampleMatrix);
}
```

`return 0;`

`}`

`// 用于将 3 x 5 数组乘以标量的函数`

```c
void scalarMultiply(int matrix[3][5], int scalar)
{
    int row, column;

    for ( row = 0; row < 3; ++row )
       for ( column = 0; column < 5; ++column )
           matrix[row][column] *= scalar;
}
```

```c
void displayMatrix(int matrix[3][5])
{
    int row, column;

    for ( row = 0; row < 3; ++row) {
        for ( column = 0; column < 5; ++column )
           printf ("%5i", matrix[row][column]);
        printf ("\n");
    }
}
```

原始矩阵：

| 7 | 16 | 55 | 13 | 12 |
|---|----|----|----|----|
| 12 | 10 | 52 | 0 | 7 |
| -2 | 1 | 2 | 4 | 9 |

乘以 2 后：

| 14 | 32 | 110 | 26 | 24 |
|----|----|-----|----|----|
| 24 | 20 | 104 | 0 | 14 |
| -4 | 2 | 4 | 8 | 18 |

再乘以 -1 后：

| -14 | -32 | -110 | -26 | -24 |
|-----|-----|------|-----|-----|
| -24 | -20 | -104 | 0 | -14 |
| 4 | -2 | -4 | -8 | -18 |

```c
#include <stdio.h>

int main (void)
{
    void    scalarMultiply (int nRows, int nCols,
                int    matrix[nRows][nCols], int    scalar);
    void    displayMatrix (int nRows, int nCols, int    matrix[nRows][nCols]);
    int     sampleMatrix[3][5] =
    {
        {   7, 16, 55, 13, 12 },
        {  12, 10, 52,   0,   7 },
        {  -2,  1,  2,   4,   9 }
    };

    printf ("Original matrix:\n");
    displayMatrix (3, 5, sampleMatrix);

    scalarMultiply (3, 5, sampleMatrix, 2);

    printf ("\nMultiplied by 2:\n");
    displayMatrix (3, 5, sampleMatrix);
}
```
