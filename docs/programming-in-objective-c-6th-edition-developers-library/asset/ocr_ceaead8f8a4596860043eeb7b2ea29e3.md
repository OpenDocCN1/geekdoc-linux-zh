stored at that memory address is then fetched and interpreted in accordance with the type declared for the pointer variable. So, if i is of type pointer to i , the value stored in the memory address given by * is interpreted as an integer by the system. In our example, the value stored at memory address 500 is fetched and interpreted as an integer. The result of the expression is 10, and is of type i .

Storing a value in a location reference by a pointer, as in
* 
proceeds in a like manner. The contents of i is fetched and treated as a memory address. The specified integer value is then stored at that address. In the preceding statement, the integer value of 2 is, therefore, stored at memory address 500.

At times, system programmers must access particular locations inside the computer's memory. In such cases, this knowledge of the way that pointer variables operate proves helpful.

As you can see from this chapter, the pointer is a very powerful construct in C. The flexibility in defining pointer variables extends beyond those illustrated in this chapter. For example, you can define a pointer to a pointer, and even a pointer to a pointer to a pointer. These types of constructs are beyond the scope of this book, although they are simply logical extensions of everything you've learned about pointers in this chapter.

The topic of pointers is probably the hardest for novices to grasp. You should reread any sections of this chapter that still seem unclear before proceeding. Solving the exercises that follow will also help you to understand the material.

# ## Exercises

+   1. Type in and run the 15 programs presented in this chapter. Compare the output produced by each program with the output presented after each program in the text.

+   2. Write a function called i to insert a new entry into a linked list. Have the procedure take as arguments a pointer to the list entry to be inserted (of type s as defined in this chapter), and a pointer to an element in the list after which the new e is to be inserted.

+   3. The function developed in exercise 2 only inserts an element after an existing element in the list, thereby preventing you from inserting a new entry at the front of the list. How can you use this same function and yet overcome this problem? (Hint: Think about setting up a special structure to point to the beginning of the list.)

+   4. Write a function called r to remove an e from a linked list. The sole argument to the procedure should be a pointer to the list. Have the function remove the entry after the one pointed to by the argument. (Why can't you remove the entry pointed to by the argument?) You need to use the special structure you set up in exercise 3 to handle the special case of removing the first element from the list.

+   5. A doubly linked list is a list in which each entry contains a pointer to the preceding entry in the list as well as a pointer to the next entry in the list. Define the appropriate structure definition for a doubly linked list entry and then write a small program that implements a small doubly linked list and prints out the elements of the list.

+   6. Develop i and r functions for a doubly linked list that are