
`2 3 5 7 11 13 17 19 23 29 31 37 41 43 47`

`condition ? expression1 : expression2`

`sign = ( number < 0 ) ? -1 : ( ( number == 0 ) ? 0 : 1 );`

`printf("Sign = %i\n", ( number < 0 ) ? -1 : ( number == 0 ) ? 0 : 1);`

开始计算

`10 S` 将累加器设置为 10

`= 10.000000` 累加器内容

`2 /` 除以 2

`= 5.000000` 累加器内容

`55 -` 减去 55

`-50.000000`

`100.25 S` 将累加器设置为 100.25

`= 100.250000`

`4 *` 乘以 4

`= 401.000000`

`0 E` 程序结束

`= 401.000000`

计算结束。

```
for ( i = 0; i < 100; ++i )
 sum += grades[i];
```

`next_value = sorted_data[(low + high) / 2];`

```
int  values[10];

values[0] = 197;
values[2] = -100;
values[5] = 350;
values[3] = values[0] + values[5];
values[9] = values[5] / 10;
--values[2];
```

```
#include <stdio.h>

int main (void)
{
int values[10];
int index;
values[0] = 197;
values[2] = -100;
values[5] = 350;
values[3] = values[0] + values[5];
values[9] =
values[5] / 10;
--values[2];
for ( index = 0; index < 10; ++index )
printf ("values[%i] = %i\n", index, values[index]);
return 0;
}
```

`values[0] = 197`
`values[1] = -2`
`values[2] = -101`
`values[3] = 547`
`values[4] = 4200224`
`values[5] = 350`
`values[6] = 4200326`
`values[7] = 4200224`
`values[8] = 8600872`
`values[9] = 35`

```
#include <stdio.h>

int main(void)
{
	int ratingCounters[11], i, response;
	for (i = 1; i <= 10; ++i)
		ratingCounters[i] = 0;
	printf("Enter your responses\n");
	for (i = 1; i <= 20; ++i) {
		scanf("%i", &response);
		if (response < 1 || response > 10)
			printf("Bad response: %i\n", response);
		else
			++ratingCounters[response];
	}
	printf("\n\nRating\tNumber of Responses\n");
	printf("------- -------------------\n");
	for (i = 1; i <= 10; ++i)
		printf("%4i%14i\n", i, ratingCounters[i]);
	return 0;
}
```

输入您的评价

6
5
8
3
9
6
5
7
15
无效评价：15
5
5
1
7
4
10
5
5
6
8
9

| 评价 | 响应次数 |
|---|---|
| 1 | 1 |
| 2 | 0 |
| 3 | 1 |
| 4 | 1 |
| 5 | 6 |
| 6 | 3 |
| 7 | 2 |
| 8 | 2 |
| 9 | 2 |
| 10 | 1 |

// 用于生成前 15 个斐波那契数的程序
```
#include <stdio.h>

int main (void)
{
    int Fibonacci[15], i;
    Fibonacci[0] = 0;    // 根据定义
    Fibonacci[1] = 1;    // 同上
    for ( i = 2;  i < 15;  ++i )
        Fibonacci[i] = Fibonacci[i-2] + Fibonacci[i-1];
    for ( i = 0;  i < 15;  ++i )
        printf ("%i\n", Fibonacci[i]);
    return 0;
}
```

```
#include <stdio.h>
#include <stdbool.h>

// 修改后的生成素数的程序
int main (void)
{
    int p, i, primes[50], primeIndex = 2;
    bool isPrime;
    primes[0] = 2;
    primes[1] = 3;
    for ( p = 5;  p <= 50;  p = p + 2 ) {
        isPrime = true;
        for ( i = 1;  isPrime  && p / primes[i] >= primes[i]; ++i )
            if ( p % primes[i] == 0 )
                isPrime = false;
        if ( isPrime == true ) {
            primes[primeIndex] = p;
            ++primeIndex;
        }
    }
    for ( i = 0;  i < primeIndex;  ++i )
        printf ("%i ", primes[i]);
    printf ("\n");
    return 0;
}
```

`2 3 5 7 11 13 17 19 23 29 31 37 41 43 47`

`int counters[5] = { 0, 0, 0, 0, 0 };`
`int integers[5] = { 0, 1, 2, 3, 4 };`
`char letters[5] = { 'a', 'b', 'c', 'd', 'e' };`
`float sample_data[500] = { 100.0, 300.0, 500.5 };`

```
float sample_data[500] = { [2] = 500.5, [1] = 300.0, [0] = 100.0 };
```

`int   x = 1233;`
`int  a[10] =   {  [9] = x + 1, [2] = 3, [1] = 2, [0] = 1 };`

```
#include <stdio.h>

int main (void)
{
    int array_values[10] = { 0, 1, 4, 9, 16 };
    int i;
    for ( i = 5; i < 10; ++i )
        array_values[i] = i * i;
    for ( i = 0; i < 10; ++i )
    printf ("array_values[%i] = %i\n", i, array_values[i]);
    return 0;
}
```

`array_values[0] = 0`
`array_values[1] = 1`
`array_values[2] = 4`
`array_values[3] = 9`
`array_values[4] = 16`
`array_values[5] = 25`
`array_values[6] = 36`
`array_values[7] = 49`
`array_values[8] = 64`
`array_values[9] = 81`

```
#include <stdio.h>

int main(void)
{
    char word[] = {'H', 'e', 'l', 'l', 'o', '!'};
    int i;
    for(i = 0; i < 6; ++i)
        printf("%c", word[i]);
    printf("\n");
    return 0;
}
```
