
# USING VIRTUAL BASE CLASSES

Derived classes and their bases form a class hierarchy that can grow tremendously complex even in relatively simple programs. A base class can be inherited by one or more other classes that in turn can become base classes for still more classes. All these classes are consequently related by single or multiple inheritance as though they were biblical characters begetting one another until no one can tell who is related to whom.

It’s easy to understand how conflicts arise in such a complex class family tree, especially when multiple inheritance is involved. One of the most common conflicts occurs when a derived class inherits too many copies of a particular base—like lottery winners, for example, who suddenly acquire more “cousins” than they previously knew existed.

To demonstrate how derived classes can get into inheritance trouble, examine the classes from the following program in Listing 15.8, franch.cpp. The program uses familiar relationships between fictitious companies and three fictitious franchisees: Bob, Ted, and Alice. The program might seem a bit silly, but borrowing familiar relationships from the real world helps to explain a typical and often exasperating problem with multiple inheritance.

```
// LISTING 15.8    FRANCH.CPP
#include <iostream.h>
#include <string.h>    // Need strlen(), strcpy()
#include <stdlib.h>    // Need free()

class Company {
private:
    char *name;
public:
    Company(const char *s) {
        name = new char[strlen(s) + 1];
        strcpy(name, s);
        cout << " In constructor for " << name;
        Display();
    }
    virtual ~Company() {
        cout << " In destructor for ";
        Display();
        delete[] name;
    }
    void Display() { cout << name << endl; }
};
```

## LISTING 15.8 CONTINUED

```
class Jennys: public Company {
public:
    Jennys(): Company("Jenny's") { }
};

class McDoughles: public Company {
public:
    McDoughles(): Company("McDoughles") { }
};

class BurgerQueen: public Company {
public:
    BurgerQueen(): Company("BurgerQueen") { }
};

class Bob:
    public Jennys,
    public McDoughles { 
};

class Ted:
    public McDoughles,
    public BurgerQueen { 
};

class Alice:
    public Jennys,
    public McDoughles,
    public BurgerQueen { 
};

int main()
{
    Bob *bobp;
    Ted *tedp;
    Alice *alicep;

    cout << endl << "Initializing Bob's restaurant" << endl;
    bobp = new Bob;
    cout << "Initializing Ted's restaurant" << endl;
    tedp = new Ted;
    cout << "Initializing Alice's restaurant" << endl;
    alicep = new Alice;

    cout << endl << "Deleting Bob's restaurant" << endl;
    delete bobp;
    cout << "Deleting Ted's restaurant" << endl;
    delete tedp;
    cout << "Deleting Alice's restaurant" << endl;
    delete alicep;
    return 0;
}
```

Figure 15.1 shows the relationships among the classes in Franch.cpp. At the root of the hierarchy is the Company class, which serves as a base class for three derived classes: Jennys, McDougles, and BurgerQueen. Each of these "company" classes is derived from Company, and each class therefore inherits a name data member and a display() member function.

## Figure 15.1
The three classes Bob, Ted, and Alice are derived using multiple inheritance.

![](img/6eab91cc30158075ed10d0cabbac9029_366_0.png)

Our three adventurous investors, Bob, Ted, and Alice, are derived using multiple inheritance (refer to Listing 15.8). Class Bob derives his culinary empire from two Company classes, Jennys and McDougles. Class Ted derives his fortunes from McDougles and BurgerQueen. Alice, the most enterprising soul in the group, takes on the three Company classes: Jennys, McDougles, and BurgerQueen. When you compile and run the program with the following commands, you see a report that indicates when the constructors and destructors are called for objects created of the highest level classes, Bob, Ted, and Alice:

```
$ g++ franch.cpp
$ ./a.out
```

Although I don't show the program's lengthy output here, onscreen you see the results of creating objects with a statement such as

```
bobp = new Bob;
...
delete Bob;
```

As you see onscreen when you run the program, all the proper constructors and destructors for the complex class hierarchy are called. So far, so good. But a subtle problem with the class relationships arises if another class is derived from the group of companies and investors. Suppose that a corporation purchases some of the parent companies and selected franchisees. As in the real world of corporate finance, the complex relationships among companies and people can easily get out of hand. Consider a Corporation class that attempts with multiple inheritance to inherit the McDougles company along with franchisees Ted and Alice:

```
class Corporation:
    public McDougles,    // ???
    public Ted,
    public Alice {
};
```

Refer to Figure 15.1 and you can see why this Corporation can never get off the ground. This is because Ted and Alice already derive in part from McDougles. When Corporation
