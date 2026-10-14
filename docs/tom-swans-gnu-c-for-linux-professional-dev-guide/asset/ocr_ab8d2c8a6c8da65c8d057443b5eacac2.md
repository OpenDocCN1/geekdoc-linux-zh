this case, the sample program creates an integer list container equal to the combined sizes of the two source lists and initializes all values in the new list to zero:

```
list<int> list4(list2.size() + list3.size(), 0);
```

Following that, the program calls merge() as follows to merge list2 into list3 and save the results in list4:

```
merge(list2.begin(), list2.end(),
list3.begin(), list3.end(), list4.begin());
```

The first two iterators define the range of elements in list2. Similarly, the next two iterators define the range of elements in list3. The last argument specifies the starting location in the destination container, here the beginning of list4. After this statement, list4 contains the sequence 1, 2, ..., 9. The containers list2 and list3 are unchanged.

> Note
> Merging is a stable operation. This means that, after merging, any duplicated objects retain their original relative order in the container.

# SET ALGORITHMS

Algorithms:

+   - set_union()
+   - set_intersection()
+   - set_difference()
+   - set_symmetric_difference()
+   - includes()

Sample program:

```
set-ex.cpp
```

As described in Chapter 24, “Building Standard Containers,” under “Sets and Multisets,” the set container does not provide operators such as union, intersection, and others. This is because sets are merely ordered containers of objects—they are not sets in a mathematical sense. To provide for the logical operations commonly applied to such sets of data, the STL provides general-purpose algorithms that work on any ordered data collection. You may use these algorithms with set containers, but you may also use them with vectors, lists, and any other containers whose data objects can be maintained in some logical order.

The four basic set algorithms are set_union(), set_intersection(), set_difference(), and set_symmetric_difference(). These all take the same general form shown here for set_union(), defined as follows:

```
OutputIterator set_union(
InputIterator1 first1, InputIterator1 last1,
InputIterator2 first2, InputIterator2 last2,
OutputIterator result [, Compare comp ])
```