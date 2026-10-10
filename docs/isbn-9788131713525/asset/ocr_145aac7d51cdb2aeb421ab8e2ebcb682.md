The default columns from Listing 13-10 are the PID, the user, the process priority, the process nice value, the virtual memory used by the process, the resident memory footprint, the amount of shared memory used by the task, and other fields that are identical to those described in the previous ps example.

Space permits only a cursory introduction to these useful utilities. You are encouraged to spend an afternoon with the man pages for top and ps to explore the richness of their capabilities.

# 13.4.6 mtrace

The mtrace package is a simple utility that analyzes and reports on calls to malloc(), realloc(), and free() in your application. It is easy to use and can potentially help spot trouble in your application. As with other userland tools we have been describing in this chapter, you must have the mtrace package configured and compiled for your architecture. mtrace is a malloc replacement library that is installed on your target. Your application enables it with a special function call. Your embedded Linux distribution should contain the mtrace package.

To demonstrate this utility, we created a simple program that creates dynamic data on a simple linked list. Each list item was dynamically generated, as was each data item we placed on the list. Listing 13-11 reproduces the simple list structure.

# Listing 13-11

Simple Linear Linked List

```
```
struct blist_s (
    struct blist_s *next;
    char *data_item;
    int item_size;
    int index;
);
```
```

Each list item was dynamically created using malloc() as follows and subsequently placed at the end of the linked list:

```
```c
struct blist_s *p = malloc( sizeof(struct blist_s) );
```
```

Each variable-sized data item in the list was also dynamically generated and added to the list item before being placed at the end of the list. This way, every list