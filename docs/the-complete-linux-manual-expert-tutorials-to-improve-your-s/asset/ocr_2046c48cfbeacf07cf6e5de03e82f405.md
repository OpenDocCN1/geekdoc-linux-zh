# Structure of a C++ Program

# COMMENTS

Lines that begin with a double slash are comments. This means they won’t be executed in the code and are ignored by the compiler. Comments are designed to help you, or another programmer looking at your code, and explain what’s going on. There are two types of comment: /* covers multiple line comments and // a single line.

```
helloworld.cpp
1 #include <iostream>
2
3 int main()
4 {
5     //My first C++ program
6
7 }
8
```

# <<

The two chevrons used here are insertion operators. This means that whatever follows the chevrons is to be inserted into the std::cout statement. In this case they’re the words ‘Hello, world’ which are to be displayed on the screen when you compile and execute the code.

```
helloworld.cpp
1 #include <iostream>
2 using namespace std;
3
4 int main()
5 {
6     //My first C++ program
7     cout << |
8 }
9
```

# STD

While std stands for something quite different, in C++ it means Standard. It’s part of the Standard Namespace in C++, which covers a number of different statements and commands. You can leave the std:: part out of the code but it must be declared at the start with: using namespace std; not both. For example:

```
#include <iostream>
using namespace std;
```

```
helloworld.cpp
1 #include <iostream>
2
3 int main()
4 {
5     //My first C++ program
6     std::cout << "Hello, world!\n";
7 }
8
```

# OUTPUTS

Leading on, the "Hello, world!" part is what you want to appear on the screen when the code is executed. You can enter whatever you like, as long as it’s inside the quotation marks. Sometimes brackets are needed, depending on the compiler. The \n part indicates a new line is to be inserted.

```
//My first C++ program
cout << "Hello, world!\n"|
```

# COUT

In this example we’re using cout, which is a part of the Standard Namespace, hence why it’s there, as you’re asking C++ to use it from that particular namespace. Cout means Character OUTput, which displays, or prints, something to the screen. If you leave std:: out you have to declare it at the start of the code, as mentioned previously.

```
helloworld.cpp
1 #include <iostream>
2 using namespace std;
3
4 int main()
5 {
6     //My first C++ program
7     cout |
8 }
9
```

# ; AND }

Finally you can see that lines within a function code block (except comments) end with a semicolon. This marks the end of the statement; all statements in C++ must have one at the end or the compiler fails to build the code. The very last line has the closing brace to indicate the end of the main function.

```
helloworld.cpp
1 #include <iostream>
2 using namespace std;
3
4 int main()
5 {
6     //My first C++ program
7     cout << "Hello, world!\n";
8 }
9
```