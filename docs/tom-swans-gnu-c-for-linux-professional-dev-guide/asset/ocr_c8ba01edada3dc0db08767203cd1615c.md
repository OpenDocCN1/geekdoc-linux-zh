The STL's removal algorithms provide several different ways to remove and erase objects in containers, the simplest and most basic of which is remove(). The algorithm is defined as follows:

```
ForwardIterator remove(
ForwardIterator first, ForwardIterator last,
const T& value)
```

Two iterators specify the range of objects to be searched for a specified value—the one to remove from the container. To demonstrate how to use remove(), the sample program creates an array container of 10 integer values, using a vector template:

```
int data[] = { 1, 2, 3, 4, 5, 6, 7, 8, 9, 10 };
vector<int> array(data, data + 10);
```

The program demonstrates one idiosyncrasy with remove(). Calling remove() with a search argument of 6

```
remove(array.begin(), array.end(), 6);
```

removes that value but doesn't adjust the resulting array. Because of that, the container now has the values
1 2 3 4 5 7 8 9 10 10

The duplicated 10 at the end of the container is the result of remove() deleting the value 6 and moving other values up one notch. However, the final value also needs erasing. Do that by instead calling remove() as follows and save the result, an iterator, in a variable:

```
vector<int>::iterator start =
remove(array.begin(), array.end(), 6);
```

The iterator, start, is of the iterator type exported by the container class. To clean up the final container, pass the iterator returned by remove(), along with a second iterator that defines the end of the range (usually the end of the container), to the container's erase() function:

```
array.erase(start, array.end());
```

Now the array correctly holds nine values. On the other hand, perhaps you don't want to erase the leftover value. In that case, you could set it to zero:
*start = 0;

> Tip
> Keep in mind that remove() affects only the target value, not any others in a container. Removing an object from a container then usually requires a follow-up operation on the remaining values. This is, however, always optional.