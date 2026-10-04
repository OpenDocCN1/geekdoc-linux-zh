```
main()
{
    char message[] = "Print straight to console\n";
    
    if (printcons(message, strlen(message))==-1)
        printf("Error occurred in printcons() call\n");
}
```

The _syscall2() macro is used here because our system call has two parameters. The macro itself will be expanded into a function in your program called printcons() which the subsequent call inside main() will execute. The preprocessor generated code inside the printcons() function in your program will contain all the necessary machine code instructions to load the appropriate CPU registers with your system call's parameter values and then execute the int 0x80 exception. When the exception returns, the return value from your kernel function will be examined and an appropriate value returned to your code in main().