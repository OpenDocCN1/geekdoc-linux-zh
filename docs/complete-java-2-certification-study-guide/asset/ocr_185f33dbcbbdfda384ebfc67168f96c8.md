# Lists

Lists are the most straightforward of Java's collections. A List keeps it elements in the order which they were added. Each element of a List has an index, starting from 0. So you can think of a List as something like an array that grows as needed (and can't contain primitives).

The Java.utilList contains a few methods in addition to those inherited from the Java.util.Collection interface. These include

```
void add(int index, Object x) // Inserts at index. The index of each subsequent element is increased by one, so indices remain
```

```
Object get(int index) // Returns the element at index.
```

```
int indexOf(Object x) // Returns the index of the first occurrence of x, or -1 if the List does not contain x
```

```
Object remove(int index) // Removes the element at index. The index of each subsequent element is reduced by one, so indices remain
```

The most common class that implements List is Vector, which provides a straightforward implementation of the interface. The methods of Vector are synchronized so that multiple threads accessing a single instance don't have to worry about corrupting the vector's contents. The following code shows the wrapped elements 101 through 110 in a Vector and uses an Iterator to retrieve and print them:

+   1. for (int i=101; i<=110; i++)
2. vec.add(i);
3.
4. Iterator iter = vec.iterator();
5. while (iter.hasNextNext())
6. System.out.println(iter.next());

Line 2 looks like an int to the Vector, which stores primitives; they store only object references. List 2 takes advantages of boxing the int to the corresponding Integer. The code is equivalent to

```
vec.add(new Integer(i));
```

In addition to Vector, three other classes in java.util List. These are Stack, ArrayList, and LinkedList. The first two are simple. Stack extends Vector, adding push(Object), pop(), and peek(Object) methods to support classic stack behavior. ArrayList is nearly identical to Vector, but its methods are not synchronized.

LinkedList is an implementation that is used to support the operations of classic linked list and double-ended queue data structures. In addition to the methods of the List interface, LinkedList has methods addFirst(), getLast(), getFirst(), getLast(), removeFirst(), and removeLast(). These let you append, retrieve, and remove at either end of the List.