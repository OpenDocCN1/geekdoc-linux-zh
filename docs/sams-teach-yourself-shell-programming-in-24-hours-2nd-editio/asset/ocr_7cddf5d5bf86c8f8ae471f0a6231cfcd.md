# Listing Filenames Only

Sometimes you don't really care about the actual lines in a file that match a particular word. You just want a list of all the files that contain that word. For example, the following command looks for the word delete in all the files in the projects directory:

```
$ grep delete projects/*
```

In this case, it produces the following output:

```
poops.c:/* Function to delete a node from the heap. Adapted from
*introduction
poops.c:void heap_delete(binary_heap *a,int i) {
poops.c: node deleted;
poops.c: /* return void if an error if the input is invalid, ie trying
*to delete
poops.c: sprint(messages,"heap_delete()"); hd, no such element.",i);
poops.c: /* switch the item to be deleted with the last item, and
*then
poops.c: deleted = a->elements[i];
poops.c: /* compare priority(a->elements[i][deleted]) ? heap_
*up(a,i); heap_down(a,i); */
poops.c:heap_delete(binary_heap *a,int i) {
scheduler.c: /* if the requested id is in the heap, delete it */
scheduler.c: heap_delete(any_heap,node_num);
```

As you look at the output, you see that only three files—poops.c, poops.h, and scheduler.c—contain the word delete. Here you had to generate a list of matching lines and then manually look at the filenames in which those lines were contained. By using the -l option of the grep command, you can reach this conclusion much faster. For example, the following command

```
$ grep -l delete projects/*
```

```
poops.c
poops.h
scheduler.c
```

produces the list you wanted.

# Counting Words

Counting words is an essential capability in shell scripts. There are many ways to do it, with the easiest being the wc command. Unfortunately, it displays only the number of characters, words, or lines. What about when you need to count the number of occurrences of a particular word in a file? The wc command falls short. In this section, you will solve this problem using the following commands:

+   - tr