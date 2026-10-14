```
char buffer[sizeof(TPersist)];

int main()
{
    TPersist *p = new(buffer) TPersist(10, 20);
    cout << *p << endl;
    cout << "Address of buffer = " << &buffer << endl;
    cout << "Address of *p   == " << &( *p) << endl;
    p->~TPersist();  // Explicit call to destructor
    // p->TPersist::~TPersist(); // For older compilers
    cout << "After calling destructor:" << endl;
    cout << *p << endl;
    return 0;
}

ostream& operator<<(ostream& os, TPersist &p)
{
    os << "x == " << p.x << ", y == " << p.y;
    return os;
}
```

Class TPersist overloads the new operator in an unusual way. Rather than allocate memory to an object pointer, the overloaded operator simply returns its void pointer parameter p. To construct an object using new, and store that object in a known location, the main program executes the following statement:

TPersist *p = new(buffer) TPersist(10, 20);

The expression new(buffer) calls the overloaded new operator for TPersist and passes the address of buffer (an array of char) as an argument. Because the overloaded operator simply returns that address, this strange-looking statement in effect assigns buffer's address to p and also calls the TPersist constructor to initialize the newly allocated object stored inside the buffer.

When you compile and run the program, it displays the address of the object in two ways and also shows the object's x and y values before and after its class destructor is called:

$ g++ persist.cpp
$ ./a.out
x == 10, y == 20
Address of buffer == 0x8049c68
Address of *p     == 0x8049c68
After calling destructor:
x == 0, y == 0

The two addresses are the same, proving that the TPersist object is indeed inside the program's own buffer. Because of that, it would be a mistake to delete the object. However, some means must be provided to call a destructor to clean up objects no longer needed. To do this, C++ permits the program to execute a statement such as

p->~TPersist();