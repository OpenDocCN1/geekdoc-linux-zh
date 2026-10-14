
### LISTING 24.3 — CONTINUED

```cpp
// object to give lower-numbered objects priority.

typedef priority_queue<Item, deque<Item>,
  less<Item> > ItemQueue;
//typedef priority_queue<Item, deque<Item>,
//  greater<Item> > ItemQueue;

int main()
{
  ItemQueue todo;  // Construct container

  // Insert some Item objects into the queue
  //
  todo.push(Item(1, "Clean oven"));
  todo.push(Item(8, "Cash paycheck"));
  todo.push(Item(2, "Sweep garage"));
  todo.push(Item(9, "Call mother"));

  // Display most critical object
  //
  cout << "The most critical item is:" << endl;
  cout << todo.top() << endl;

  // Display and remove objects in critical order
  //
  cout << "Removing items in critical order:" << endl;
  while (!todo.empty()) {
    cout << todo.top() << endl;
    todo.pop();
  }

  return 0;
}

// Display an Item object
ostream& operator<<(ostream& os, const Item& r)
{
  cout << "(" << r.GetWeight() << ") " << r.GetItem();
  return os;
}
```

Compile and run the todo.cpp program to display a list of chores, prioritized by number with higher-numbered items given priority. The program displays the most critical item, followed by all objects in priority order. Enter these commands:

```text
$ g++ todo.cpp
$ ./a.out
The most critical item is:
(9) Call mother
Removing items in critical order:
(9) Call mother
(8) Cash paycheck
(2) Sweep garage
(1) Clean oven
```

The program bases its priority_queue container on the STL deque template. A typedef name makes creating the actual container clearer:

```cpp
typedef priority_queue<
Item, deque<Item>, less<Item> > ItemQueue;
```

To the priority_queue template, specify three items: The type of data to store in the container (Item), the underlying data structure (deque<Item>), and a function object (less<Item>) used to maintain the order of objects in the queue. Change less to greater to order entries from low to high.

The Item class represents the data to store in the queue. The class declares a weight and a string that describes the job to be done. The most important member of the Item class is its overloaded operator<() function. When designing your own priority_queue data objects, your class needs an operator similar to this one:

```cpp
bool operator< (const Item& arg) const
{ return weight < arg.weight; }
```

The overloaded operator's parameter is a constant reference to an object of the class type. The operator itself is const because it makes no changes to Item's data members. Return a true value if the priority of the current object—the one for which the operator function is called—is less than the priority of the parameter (arg in this example).

> Tip
> You do not need to overload the greater-than operator even if you change the ordering. Only the less-than operator is needed in the class of object to be stored in the queue.

Given the ItemQueue typedef name, creating the container is easy:

```cpp
ItemQueue todo;
```

To insert objects into the todo container, call the push() member function like this:

```cpp
todo.push(Item(1, "Clean oven"));
...
todo.push(Item(9, "Call mother"));
```

The integer values represent the weights, and the strings of course describe each entry. You can use any type of data for either element simply by changing the Item class's members. No changes to the priority_queue template are needed to accommodate other types of data.

Call the top() function to examine the most-critical object in the queue:

```cpp
cout << todo.top() << endl;
```

To remove the most critical object, call pop(). The following while loop calls that function plus empty() and top() to display all objects and empty the queue:

```cpp
while (!todo.empty()) {
  cout << todo.top() << endl;
  todo.pop();
}
```

## SUMMARY

The STL provides 10 container template classes for creating fundamental data structures such as lists, vectors, and queues. Because they are template-based, the classes can store any types of objects or pointers (but not references). The 10 standard classes are vector, list, deque, set, multiset, map, multimap, stack, queue, and priority_queue. In most cases, a class object is in a container by using one or more iterators. For this purpose, container classes export the type name iterator. Container template classes also provide several member functions you can call to sort, search, insert, and delete objects. You can also use standard algorithms to perform various actions on objects in containers as the next chapter explains.

For more information on subjects introduced in this chapter, turn to the following chapters:

- Chapter 12, “Introducing the Class”
- Chapter 17, “Creating Class Templates”
- Chapter 21, “Honing Your C++ Skills”
- Chapter 23, “Using the Standard Template Library (STL)”
- Chapter 25, “Applying Standard Algorithms”
