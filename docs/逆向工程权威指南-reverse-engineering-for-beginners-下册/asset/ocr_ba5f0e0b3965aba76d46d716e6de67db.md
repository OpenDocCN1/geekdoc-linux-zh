```
{
  MessageBox(NULL, "hello, world!", "caption",
  MB_TOPMOST | MB_ICONINFORMATION | MB_YESNOCANCEL);
}
```

#  题目4

对应章节: 19.7.4节

这个函数把两个32位数相乘，返回64位的积。解答这种题目，根据输入输出进行判断的速度比较比较快。

```
#include <stdio.h>
#include <stdint.h>

// source code taken from
//http://www.wittenberg.edu/academics/mathcomp/shelburne/comp2
55/notes/binarymultiplication.pdf

int64_t mult(uint32_t m, uint32_t n)
{
  uint64_t p = 0; // initialize p to 0
  while (n != 0) // while multiplier n is not 0
  {
    if (n & 1) // test LSB of multiplier
      p = p + m; // if 1 then add multiplicand m
    m = m << 1; // left shift multiplicand
    n = n >> 1; // right shift multiplier
  }
  return p;
}

int main()
{
  printf("%d\n", mult (2, 7));
  printf("%d\n", mult (3, 11));
  printf("%d\n", mult (4, 111));
n
```

# 第21章

# 题目1