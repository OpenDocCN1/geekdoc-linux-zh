# Structure of a C++ Program

**COMMENTS** Lines that begin with a double slash are comments. This means they won't be executed in the code and are ignored by the compiler. Comments are designed to help you, or another programmer looking at your code, and explain what's going on. There are two types of comment: `//` covers multiple line comments and `/*` a single line.

![](bbox=[0.06, 0.23, 0.47, 0.37])

The two chevr ons used here are insertion operators. This means that whatever follows the chevr ons is to be inserted into the std::cout statement. In this case they're the words ‘Hello, world’ which are to be displayed on the screen when you compile and execute the code.

![](bbox=[0.52, 0.23, 0.93, 0.37])

**STD** While std stands for something quite different, in C++ it means Standard. It's part of the Standard Namespace in C++, which covers a number of different statements and commands. You can leave the std:: part out of the code but it must be declared at the start with: using namespace std; not both. For example:

```
#include <iostream>
using namespace std;
```

![](bbox=[0.06, 0.54, 0.47, 0.67])

**OUTPUTS** Leading on, the “Hello, world!” part is what you want to appear on the screen when the code is executed. You can enter whatever you like, as long as it's inside the quotation marks. Sometimes brackets are needed, depending on the compiler. The \n part indicates a new line is to be inserted.

![](bbox=[0.52, 0.49, 0.93, 0.67])

**COUT** In this example we're using cout, which is a part of the Standard Namespace, hence why it's there, as you're asking C++ to use it from that particular namespace. Cout means Character OUtput, which displays, or prints, something to the screen. If you leave std:: out you have to declare it at the start of the code, as mentioned previously.

![](bbox=[0.06, 0.8, 0.47, 0.93])

**;AND }** Finally you can see that lines within a function code block (except comments) end with a semicolon. This marks the end of the statement; all statements in C++ must have one at the end or the compiler fails to build the code. The very last line has the closing brace to indicate the end of the main function.

![](bbox=[0.52, 0.8, 0.93, 0.93])