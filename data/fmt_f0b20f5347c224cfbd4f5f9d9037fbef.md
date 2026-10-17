
`scalarMultiply`(3, 5, `sampleMatrix`, -1);

`printf`("\nThen multiplied by -1:\n");

`displayMatrix`(3, 5, `sampleMatrix`);

`return` 0;

// 用于将矩阵乘以标量的函数

```c
void scalarMultiply (int nRows, int nCols,
                    int matrix[nRows][nCols], int  scalar)
{
  int  row, column;
  for (  row = 0;  row < nRows;  ++row )
    for (  column = 0;  column < nCols;  ++column )
      matrix[row][column]  *=  scalar;
}
```

```c
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

原始矩阵：

```
  7  16  55   13   12
 12  10  52    0    7
 -2   1   2    4    9
```

乘以 2 后：

```
 14  32  110   26   24
 24  20  104    0   14
 -4   2    4    8   18
```

再乘以 -1 后：

```
-14  -32  -110  -26  -24
-24  -20  -104    0  -14
  4   -2    -4   -8  -18
```

`void scalarMultiply (int nRows, int nCols, int matrix[nRows][nCols], int scalar)`

`void scalarMultiply (int matrix[nRows] [nCols], int nRows, int nCols, int scalar)`

### 将正整数转换为其他进制的程序

```c
#include <stdio.h>

int        convertedNumber[64];
long int   numberToConvert;
int        base;
int        digit = 0;

void getNumberAndBase (void)
{
   printf ("Number to be converted? ");
   scanf ("%li", &numberToConvert);
   printf ("Base? ");
   scanf ("%i", &base);
   if ( base < 2 || base > 16 ) {
      printf ("Bad base - must be between 2 and 16\n");
      base = 10;
   }
}

void convertNumber (void)
{
   do {
      convertedNumber[digit] = numberToConvert % base;
      ++digit;
      numberToConvert /= base;
   }
   while ( numberToConvert != 0 );
}

void displayConvertedNumber (void)
{
	const char baseDigits[16] =
	{ '0', '1', '2', '3', '4', '5', '6', '7',
	  '8', '9', 'A', 'B', 'C', 'D', 'E', 'F' };
	int nextDigit;
	printf ("Converted number = ");
	for (--digit; digit >= 0; --digit ) {
		nextDigit = convertedNumber[digit];
		printf ("%c", baseDigits[nextDigit]);
	}
	printf ("\n");
}

int main (void)
{
	void getNumberAndBase (void), convertNumber (void),
	     displayConvertedNumber (void);
	getNumberAndBase ();
	convertNumber ();
	displayConvertedNumber ();
	return 0;
}
```

要转换的数字？ 100

基数？ 8

转换后的数字 = 144

要转换的数字？ 1983

基数？ 0

无效的基数 - 必须在 2 到 16 之间

转换后的数字 = 1983

`int		gConvertedNumber[64];`

`long int	gNumberToConvert;`

`int		gBase;`

`int		gDigit = 0;`

`nextMove = gCurrentMove + 1;`

```c
float squareRoot (float x)
{
 const float epsilon = .00001;
 float guess = 1.0;
 ...
}
```

### 用于演示静态变量和自动变量的程序

```c
#include <stdio.h>

void auto_static (void)
{
	int		autoVar = 1;
	static int	staticVar = 1;
	printf ("automatic = %i, static = %i\n", autoVar, staticVar);
	++autoVar;
	++staticVar;
}

int main (void)
{
	int	i;
	void auto_static (void);
	for ( i = 0; i < 5; ++i )
		auto_static ();
	return 0;
}
```

automatic = 1, static = 1

automatic = 1, static = 2

automatic = 1, static = 3

automatic = 1, static = 4

automatic = 1, static = 5

5! = 5 x 4 x 3 x 2 x 1

= 120

6! = 6 x 5 x 4 x 3 x 2 x 1

= 720

```c
#include <stdio.h>

int main (void)
{
    unsigned int    j;
    unsigned long int    factorial (unsigned int   n);
    for ( j = 0;   j < 11;   ++j )
        printf ("%2u! = %lu\n", j, factorial (j));
    return 0;
}
```

// 递归函数，用于计算正整数的阶乘

```c
unsigned long int   factorial (unsigned int   n)
{
    unsigned long int   result;
    if ( n == 0 )
        result = 1;
    else
        result = n * factorial (n - 1);
    return result;
}
```

`factorial`(3) = 3 * `factorial`(2)

    = 3 * 2 * `factorial`(1)

    = 3 * 2 * 1 * `factorial`(0)

    = 3 * 2 * 1 * 1

    = 6

$lcm(u,v) = uv / gcd(u,v)$

$u,v >= 0$

`int month = 9, day = 25, year = 2015;`

`struct date  today, purchaseDate;`

`if ( today.month == 1 && today.day == 1 )`

    `printf` ("Happy New Year!!\n");

// 用于演示结构体的程序

```c
#include <stdio.h>

int main (void)
{
    struct date
    {
        int month;
```
