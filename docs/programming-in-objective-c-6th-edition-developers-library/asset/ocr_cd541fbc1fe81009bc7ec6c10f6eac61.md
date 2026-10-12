```
```
##
/
s{


}
```
```

If the allocation succeeds, a null pointer is placed in the n        member of the newly allocated linked-list entry (pointed to by 1                ).

The function returns a pointer to the new list entry, or the null pointer if the allocation fails (verify that this is, in fact, what happens). If you draw a picture of a linked list and trace through the execution of a               , it will help you to understand how the function works.

Another function, called r               , is associated with dynamic memory allocation. It can be used to shrink or expand the size of some previously allocated storage. For more details, consult Appendix B.

This chapter concludes coverage of the features of the C language. In Chapter 17, “Debugging Programs,” you learn some techniques that will help you to debug your C programs. One involves using the preprocessor. The other involves the use of a special tool, called an interactive debugger.

# Exercises

+   1. Type in and run the program presented in this chapter. Check the program’s results by comparing the original file you chose to copy with the filename you entered to copy and ensure the two are the same.

+   2. Finish the program that takes a word as a command-line argument and looks up the word to see whether it is in the array of terms and definitions, providing the definition if it is found, or informs the user that the term is not in the program’s glossary if it isn’t found.