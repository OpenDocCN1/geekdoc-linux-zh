
- The class containing the private and protected data is the one that declares another class to be a friend, thus giving that friend special access to the normally hidden members of the declaring class. A class can never declare itself to be a friend of another class—that would be like inviting yourself to dinner at a stranger’s house.

- A friend class might be declared before or after the class that declares the friend. The order of declarations is unimportant, but the friend class is typically declared last so that any member functions in the friend class can refer to the other class’s private and protected elements.

- Derived classes of the friend do not inherit special access to the original class’s private and protected members. Only the specifically named friend class has that permission.

- A derived class might be a friend of its base class, although in such cases, using protected members in the base accomplishes the same goal of giving the derived class (the friend) access to restricted members in the base class.

Listing 18.1, friend.cpp, demonstrates how a friend class can access another class’s private and protected members.

## LISTING 18.1 FRIEND.CPP

```
#include <iostream.h>
#include <string>    // Need string class

class Pal {
    friend class Buddy;  // Buddy is a friend of Pal
private:
    string label;
protected:
    void Putlabel(string arg) { label = arg; }
public:
    Pal(string arg): label(arg) { }
};

class Buddy {
private:
    Pal palObject;
public:
    Buddy(string arg): palObject(arg) { }
    void FriendDemo();
};

int main()
{
    Buddy aBuddy("First Message");
    aBuddy.FriendDemo();
    return 0;
}

// Demonstrate how Buddy object can access Pal private
// and protected members
void Buddy::FriendDemo()
{
```

```
cout << "Reading private Pal::message from Buddy" << endl;
cout << palObject.label << endl;
cout << "Calling protected Pal::PutLabel function" << endl;
palObject.PutLabel("Second Message");
cout << palObject.label << endl;
cout << "Writing private Pal::message from Buddy" << endl;
palObject.label = "Third Message";
cout << palObject.label << endl;
}
```

Compile and run the program in the usual way. Its output shows how a friend class can access a private string label in another class:

```
$ g++ friend.cpp
$ ./a.out
Reading private Pal::message from Buddy
First Message
Calling protected Pal::PutLabel function
Second Message
Writing private Pal::message from Buddy
Third Message
```

In the friend.cpp program, class Pal declares Buddy as a friend. This gives Buddy access to Pal's private string label data member and also its PutLabel() protected member function. The Pal class also declares a constructor, but it provides no other access to its private and protected members. A program statement could construct a Pal object like this:

```
Pal palObject("A String");
```

But that's all it could do. Because Pal provides no functions to read and write its data, the only possible operation is to construct an object of type Pal. However, because Buddy is a friend of Pal, it can access Pal's normally hidden declarations. To demonstrate, the sample program creates an object of type Buddy and calls its FriendDemo() member function:

```
Buddy aBuddy("First Message");
aBuddy.FriendDemo();
```

## MUTUAL FRIEND CLASSES

Two classes can declare each other as friends, giving each class access to the other's private and protected members. This is the object-oriented equivalent of two people staying in adjacent hotel rooms and keeping the inner door open. Outsiders can't see what's going on inside, but the two guests are free to visit each other's rooms.

Using mutual friend classes destroys the barriers that normally prohibit access to a class's restricted members, and it's rare that you'll use this technique. It is occasionally useful, however, to provide mutual access to static data members among two classes. Listing 18.2, mutual.cpp, demonstrates the basic technique.

## LISTING 18.2 MUTUAL.CPP

```
#include <iostream.h>

class BClass;

class AClass {
    friend BClass;
private:
    static int x;
public:
    AClass(int arg) { x = arg; }
    void AFunction();
};

class BClass {
    friend AClass;
private:
    static int y;
public:
    BClass(int arg) { y = arg; }
    void BFunction();
};

int AClass::x;
int BClass::y;

int main()
{
    AClass a(123);
    BClass b(456);
    a.AFunction();
    b.BFunction();
    return 0;
}

void AClass::AFunction()
{
    cout << "Inside AClass::AFunction()" << endl;
    cout << "x == " << x << "; y == " << BClass::y << endl;
}

void BClass::BFunction()
```
