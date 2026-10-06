# A SIMPLE LINKED LIST

# Head

# Tail

![](bbox=[0.104, 0.247, 0.896, 0.301])

> Linked lists are generic enough to be used in many different situations

Two functions create.c: insert() and lookup() are used for adding a new node and looking up an element value in the list, respectively. Both functions take two arguments: the head of the linked list and the data (value) and return an integer, which is 1 in case of success and 0 in case of failure. The insert function determines whether the data already exists in the list, in order to make the lookup() the most important function of the program.

No operation on a linked list can be completed without traversing it. The traverse() function visits all the nodes and writes them to a file that each node occupies a separate line and populates the linked list with them. The name of the file is given as a command line argument.

Above Each of the five nodes in the linked list contains value and a link to another node

```
typedef struct node {
    char *data;
    struct node *next;
};
```

The next pointer of the last node points to NULL in order to indicate that we have reached the end of the list. The defined structure has only one variable for storing data, but you are free to declare numerous variables inside the node structure. The create() function allocates the memory for a new node and returns the following:

```
new_node = malloc(sizeof(*node));
if (new_node == NULL) {
    return 0;
}
```

A successful call to malloc returns a pointer to the allocated memory. If there is an error, malloc() returns NULL. The two lines of code are used for checking the return value of malloc(). Once a new node is created, you will also need to allocate memory for the data because it is a string pointer, which is done with the following:

```
new_node->next = next;
*list = new_node;
```

Download and free the code in FileSize. Each new node is inserted at the front of the unsorted linked list and becomes the head of the linked list:

It is time to take a little bit more about the linked list implementation of create.c, which is the base of this tutorial.

# Creating a sorted list

Linked lists not help you sort your data easily, but also help you keep your data sorted after inserting or deleting. Deleting from an unsorted list is the same as above; however, inserting into a sorted list is

# Advantages and disadvantages

Linked lists are good for sequential searching, especially when there are many insertions and deletions. If the list has many elements, the search time of the element can be very slow.

Additionally, unsorted lists can be very slow when searching for an element. An unsorted linked list with 150,000 nodes will be very slow! Also, linked lists have an advantage: unlike arrays, they can add or remove elements from them.

As you can appreciate, sorted lists have many advantages. However, inserting into a sorted list is costly, so to keep your list sorted when possible. However, inserting into a sorted list is not easy.
If you need to manage a large number of sorted elements and to search them fast, then you'd better use a tree structure instead of a linked list; the price you are going to pay is that you will lose the simplicity of the linked list; however, you will need more memory to create and keep a tree or a hash table sorted or balanced.