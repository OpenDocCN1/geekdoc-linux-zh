For list- or deque-based stacks, include those headers as well. To create a stack container, specify the type of data to store and type of structure to use for maintaining the stack:

```
stack<int, vector<int> > int_stack;
```

That works just fine, but a typedef declaration helps clarify the programming:

```
typedef stack<int, vector<int> > TIntStack;
```

That makes TIntStack a stack class that can store int values and that uses an integer vector as its storage mechanism. You can now construct the actual container with a simple statement such as this:

```
TIntStack int_stack;
```

# USING STACKS

To insert values into a stack, call the push() function as in this loop:

```
for (int i = 1; i < 10; i++)
    int_stack.push(i);
```

Call top() to refer to the top object on the stack—the only object available for use. (In its classic form, a stack prevents access to any other objects.) Call pop() to remove the top object. Call empty() to determine whether the stack is empty. Together, the three functions can pop and display all values pushed onto the int_stack container:

```
while (!int_stack.empty()) {
    cout << int_stack.top() << " ";
    int_stack.pop();
}
```

A stack may store any kind of object. For example, include the coordinate.h header file listed in this chapter and then use a typedef declaration to create a type name for a stack of TCoordinate class objects:

```
typedef stack<TCoordinate, deque<TCoordinate> > TCoordStack;
```

Construct the stack container and fill it with TCoordinate objects using statements such as

```
TCoordStack coord_stack;
coord_stack.push(TCoordinate(10, 20));
```

The preceding while loop, along with the empty(), top(), and pop() functions, works the same for stacks of objects as it does for simple integer values. Just change the stack object name to display and remove all TCoordinate objects.

# QUEUES

There are two types of queue containers in the STL. One is based on a list. The other is based on a deque. Both types of queues provide the same operations; only their underlying data structure is selectable. For the most part, a list is the better choice for storing large objects and large numbers of objects; otherwise, a deque is potentially faster. A queue is a first-in, first-out (FIFO) data structure that works like a line at the post office. Unless the program cheats, objects enter only at the back of the line and exit at the front.