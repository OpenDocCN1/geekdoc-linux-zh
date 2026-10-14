# User Interaction

There’s nothing quite as satisfying as creating a program that responds to you. This basic user interaction is one of the most taught aspects of any language and with it you’re able to do much more than simply greet the user by name.

# HELLO, DAVE

You have already used cout, the standard output stream, throughout our code. Now you’re going to be using cin, the standard input stream, to prompt a user response.

# STEP 1

Anything that you want the user to input into the program needs to be stored somewhere in the system memory, so it can be retrieved and used. Therefore, any input must first be declared as a variable, so it’s ready to be used by the user. Start by creating a blank C++ file with headers.

```
userinteraction.cpp
1 #include <iostream>
2 using namespace std;
3 
4 int main()
5 {
6 
7 
8 
9 }
10
```

# STEP 2

The data type of the variable must also match the type of input you want from the user. For example, to ask a user their age, you would use an integer like this:

```
#include <iostream>
using namespace std;

int main ()
{
    int age;
    cout << "what is your age: ";
    cin >> age;
    cout << "\nYou are " << age << " years old.\n";
}
```

```
userinteraction.cpp
1 #include <iostream>
2 using namespace std;
3 
4 int main()
5 {
6     int age;
7     cout << "What is your age: ";
8     cin >> age;
9     
10    cout << "\nYou are " << age << " years old.\n";
11 
12 
13 }
14
```

# STEP 3

The cin command works in the opposite way from the cout command. With the first cout line you’re outputting ‘What is your age’ to the screen, as indicated with the chevrons. Cin uses opposite facing chevrons, indicating an input. The input is put into the integer age and called up in the second cout command. Build and run the code.

![](bbox=[0.44, 0.51, 0.94, 0.64])

# STEP 4

If you’re asking a question, you need to store the input as a string; to ask the user their name, you would use:

```
#include <iostream>
using namespace std;

int main ()
{
    string name;
    cout << "what is your name: ";
    cin >> name;
    cout << "\nHello, " << name << ", I hope you’re well today?\n";
}
```

```
userinteraction.cpp
1 #include <iostream>
2 using namespace std;
3 
4 int main()
5 {
6     string name;
7     cout << "What is your name: ";
8     cin >> name;
9     
10    cout << "\nHello, " << name << ", I hope you’re well today?\n";
11 
12 }
13 
14
```