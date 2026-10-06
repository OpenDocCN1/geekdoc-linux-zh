# ADDING A NEW NODE TO A LINKED LIST

![](bbox=[0.145, 0.207, 0.705, 0.283])

![](bbox=[0.11, 0.313, 0.755, 0.396])

```
int main(int argc, char *argv) {
  node *linkedList = NULL;
  int data[] = {21, -12, 56, -2, 21, 190};

  // Initialize the Linked List
  for (int i=0; i<6; i++) {
    insert(linkedList, data[i]);
  }

  printLinkedList(linkedList);
  return 0;
}
```

as fast as possible and then you sort it before you use it. This time the node structure will be as follows:

```
typedef struct node {
  int data;
  struct node *next;
};
```

The reason for using an integer instead of a string is for you to better understand the sorting process. Additionally, you will need a second malloc() as the memory for it is allocated when you delete it, so sortExisting.c will be a little bit simpler in this order. To sort a linked list, you can use a simple algorithm such as Bubble sort or Quick sort. I chose Bubble sort because it's easier to understand — Quick sort is faster.

However, the logic implemented in the (lookup) function of createNode is different from the logic in create, because it uses a search that stops as soon as the data that you are searching for is found. Compared to Bubble, it can have many swaps, but it keeps the linked list being sorted. The key point here is that the data is sorted from 'smaller' to 'larger', which helps you determine whether the data you are searching for is in the sorted list or not. This is the main benefit you get from a sorted list.

Additionally, the insertion function will differ entirely on a sorted list because it does not insert the new node in front of the linked list but puts it in the right. If you follow the code of createNode.c, you can see that the logic of the node is as follows:

# Inserting into an unsorted linked list

Inserting into a linked list is pretty easy. You can see, due to the fact that you first have to search the list in order to find if the element exists

+   Circular list

Although you usually use a single linked list, there is another kind of linked list called a circular list. The tricky part is that when you traverse a circular list, there is no NULL pointer. In a circular linked list, the last element of the tail points to the head of the list. If its double-linked, the head of the list points back to the tail as well.

# Sorting an unsorted linked list

The next C program in your FileSo (sortExisting.c) will sort a linked list that is not yet sorted — the original linked list will be manually sorted using C. This is a hybrid approach where you first create the linked list

A simple situation where a circular linked list could be useful is when you are making a game where a player starts at a stack, they can lose their turn, or ask a question of the next player, or ask a