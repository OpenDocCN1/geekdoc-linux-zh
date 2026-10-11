
## Structure of a C++ Program

C++ has a very defined structure and way of doing things. Miss something out, even as small as a semicolon, and your entire program will fail to be compiled and executed. Many a professional programmer has fallen foul of sloppy structure.

### INCLUDE <C++ STRUCTURE>

Learning the basics of programming, you begin to understand the structure of a program. The commands may be different from one language to the next but you can start to see how the code works.

![](img/4aefeb2d095f688b34af6207870c5f39_43_0.png)

- **C++**
  C++ was invented by Danish student Bjarne Stroustrup in 1979, as a part of his Ph.D. thesis. Initially C++ was called C with Classes, which added features to the already popular C programming language, while making it a more user-friendly environment through a new structure.

- **INT MAIN()**
  int main() initiates the declaration of a function, which is a group of code statements under the name ‘main’. All C++ code begins at the main function, regardless of where it actually lies within the code.

```cpp
helloworld.cpp
1  #include <iostream>
2
3  int main()
4
5
```

- **#INCLUDE**
  The structure of a C++ program is quite precise. Every C++ code begins with a directive: `#include <...>`. The directive instructs the pre-processor to include a section of the standard C++ code. For example: `#include <iostream>` includes the iostream header to support input/output operations.

```cpp
helloworld.cpp
1  #include <iostream>
2
3
4
```

- **BRACES**
  The open brace (curly brackets) is something that you may not have come across before, especially if you’re used to Python. The open brace indicates the beginning of the main function and contains all the code that belongs to that function.

```cpp
helloworld.cpp
1  #include <iostream>
2
3  int main()
4  {
5
6  }
7
8
```

### COMMENTS

Lines that begin with a double slash are comments. This means they won't be executed in the code and are ignored by the compiler. Comments are designed to help you, or another programmer looking at your code, and explain what's going on. There are two types of comment: `//` covers multiple line comments and `/*` a single line.

![](img/4aefeb2d095f688b34af6207870c5f39_44_0.png)

The two chevrons used here are insertion operators. This means that whatever follows the chevrons is to be inserted into the std::cout statement. In this case they're the words ‘Hello, world’ which are to be displayed on the screen when you compile and execute the code.

![](img/4aefeb2d095f688b34af6207870c5f39_44_1.png)

**STD** While std stands for something quite different, in C++ it means Standard. It's part of the Standard Namespace in C++, which covers a number of different statements and commands. You can leave the std:: part out of the code but it must be declared at the start with: using namespace std; not both. For example:

```cpp
#include <iostream>
using namespace std;
```

![](img/4aefeb2d095f688b34af6207870c5f39_44_2.png)

**OUTPUTS** Leading on, the “Hello, world!” part is what you want to appear on the screen when the code is executed. You can enter whatever you like, as long as it's inside the quotation marks. Sometimes brackets are needed, depending on the compiler. The \n part indicates a new line is to be inserted.

![](img/4aefeb2d095f688b34af6207870c5f39_44_3.png)

**COUT** In this example we're using cout, which is a part of the Standard Namespace, hence why it's there, as you're asking C++ to use it from that particular namespace. Cout means Character OUtput, which displays, or prints, something to the screen. If you leave std:: out you have to declare it at the start of the code, as mentioned previously.

![](img/4aefeb2d095f688b34af6207870c5f39_44_4.png)

**}; AND }** Finally you can see that lines within a function code block (except comments) end with a semicolon. This marks the end of the statement; all statements in C++ must have one at the end or the compiler fails to build the code. The very last line has the closing brace to indicate the end of the main function.

![](img/4aefeb2d095f688b34af6207870c5f39_44_5.png)

## Compile and Execute

You’ve created your first C++ program and you now understand the basics behind the structure of one. Let’s get things moving and compile and execute, or run if you prefer, the program and see how it looks.

### GREETINGS FROM C++

Compiling and executing code from within Geany is remarkably simple and just a matter of clicking a couple of icons and seeing the result. Here’s how it’s done.

**STEP 1**
Open Geany, if you haven’t already, and load up the previously saved Hello World code you created. Ensure that there are no visible errors, such as a missing semicolon at the end of the std::cout line.

![](img/4aefeb2d095f688b34af6207870c5f39_45_0.png)

**STEP 3**
When you click the Build icon, the pane at the bottom of the Geany interface displays some results. If all is well, you will see a successful compilation, if not then Geany issues an error along with the line the error was found on.

![](img/4aefeb2d095f688b34af6207870c5f39_45_1.png)

**STEP 2**
If your code is ready, look to the menu bar along the top of the Geany window. Notice that midway along the line of icons there’s a red brick icon. This is Build, which when clicked runs through the code, checking it against the C++ standards to see if there are any errors that stop it from running.

![](img/4aefeb2d095f688b34af6207870c5f39_45_2.png)

**STEP 4**
With the code successfully built, it’s now time to execute it. Next to the Build icon there’s a paper aeroplane icon, this is the Run icon. You can’t run code that hasn’t been previously built or has an error in place. Click the Run icon.

![](img/4aefeb2d095f688b34af6207870c5f39_45_3.png)

**STEP 5**
When you click Run, the C++ code executes and a simple Terminal window appears displaying the results of the code. In the case of this simple code, you can see the word: Hello, world! in the window; as you've already learned, the code is cout\t\t-ing (outputting) the contents between the quotes in the std::cout line.

![](img/4aefeb2d095f688b34af6207870c5f39_46_0.png)

**STEP 6**
Pressing Return/Enter in the command line box closes it, returning you to Geany. Let's alter the code slightly. Under the #include line, enter:

`using namespace std;`

Then, delete the std:: part of the Cout line; like so:

`cout << "Hello, world!\n";`

![](img/4aefeb2d095f688b34af6207870c5f39_46_1.png)

**STEP 7**
In order to apply the new changes you need to save the file, build it and execute it again. Go through the process as before, you don't need to change the name of the file unless you want to, of course, followed by clicking the Brick icon, then the Aeroplane icon.

![](img/4aefeb2d095f688b34af6207870c5f39_46_2.png)

**STEP 8**
Just as mentioned previously, you don't need to have std::cout if you've already declared the standard namespace at the start of the code. Now, let's create a deliberate mistake, to see what happens. Remove the semicolon from the cout line, so it reads:

`cout << "Hello, world!\n"`

![](img/4aefeb2d095f688b34af6207870c5f39_46_3.png)

**STEP 9**
Now try and build the code once more. This time, notice that the bottom panel is displaying an error, regarding the missing semicolon. Note that error reads as being on line 8, the first character, the closed curly bracket. This is because there's an expected semicolon missing before the closed bracket.

![](img/4aefeb2d095f688b34af6207870c5f39_46_4.png)

**STEP 10**
Replace the semicolon and under the cout line, enter a new line to your code:

`cout << "And greetings from C++!\n";`

The \n simply adds a new line under the last line of outputted text. Build and Run the code, to display your handiwork.

![](img/4aefeb2d095f688b34af6207870c5f39_46_5.png)

## Virus!

### DID YOU KNOW...

That one of the first programmed computer viruses that spread outside of a controlled system, i.e. into the wild, was called Elk Cloner and it was coded in 1982 by Rich Skrenta, a fifteen year old student.

Elk Cloner was programmed to infect the Apple DOS 3.3 operating system, and attached to a game. When the game was played fifty times the virus would be activated and instead of displaying the game the virus would blank the screen and display a poem:

Elk Cloner:
The program with a
personality

It will get on all
your disks
It will infiltrate your
chips
Yes, it's Cloner!

It will stick to you
like glue
It will modify RAM too
Send in the Cloner!

![](img/4aefeb2d095f688b34af6207870c5f39_47_0.png)
