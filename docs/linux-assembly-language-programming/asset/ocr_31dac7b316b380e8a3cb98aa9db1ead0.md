A recursive definition can very often be easily turned into a computationally effective, if not efficient, program. This is typically illustrated using the Fibonacci numbers.

```
1                 if k < 2
fib(k) =
         fib(k - 1) + fib(k - 2)   otherwise.
```

Program 7.9 shows how this recursive definition can be turned into C code. In assembly language, we can code this easily, provided we recall that used registers other than EAX must be pushed. Program 7.10 shows how we can get by using only ECX and EAX. To test this program from C, one can use a small calling program such as Program 7.11. To test a program like this using Edlinas, it is also necessary to initialize the stack, as is shown in the first line of Program 7.3.

# Program 7.8

```
```c
main()
{
    int count,x,y;
    count = 0;

    printf("Enter a number:  ");
    scanf("%d", &x);

    while(x != 1)
    {
        count = count + 1;
        y = half(x); /* This is the subroutine call! */
        if(y != 0)
            x = y;
        else
            x = 3*x + 1;
        printf("\n x = %d.", x);
    }
    printf("\n There were %d iterations.\n\n.",count);
}
```
```

# Program 7.9

```
```c
int fib(int k)
{
    int d;

    if(k < 2)
        d = 1;
    else
        d = fib(k-1) + fib(k-2);

    return d;
}
```
```

# Program 7.10

```
```asm
    glocal fib
fib:    PUSH ECX          ; Gives us access to ECX
        MOV EAX, [ESP + 8]
                        ; Access parameter
        CMP EAX, 2          ; if k < 2
        JAE ELS           ;
        MOV EAX, 1        ; Put the return value in EAX
        JMP DUN
ELS:    DEC EAX           ; Get k-1
        MOV ECX, EAX      ; EAX will be overwritten!
```