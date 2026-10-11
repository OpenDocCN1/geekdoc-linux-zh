
## User Interaction

There's nothing quite as satisfying as creating a program that responds to you. This basic user interaction is one of the most taught aspects of any language and with it you're able to do much more than simply greet the user by name.

### HELLO, DAVE

You have already used `cout`, the standard output stream, throughout our code. Now you're going to be using `cin`, the standard input stream, to prompt a user response.

- **STEP 1**  
  Anything that you want the user to input into the program needs to be stored somewhere in the system memory, so it can be retrieved and used. Therefore, any input must first be declared as a variable, so it's ready to be used by the user. Start by creating a blank C++ file with headers.

![](img/4aefeb2d095f688b34af6207870c5f39_59_0.png)

- **STEP 2**  
  The data type of the variable must also match the type of input you want from the user. For example, to ask a user their age, you would use an integer like this:

```cpp
#include <iostream>
using namespace std;

int main ()
{
    int age;
    cout << "What is your age: ";
    cin >> age;
    
    cout << "\nYou are " << age << " years old.\n";
}
```

![](img/4aefeb2d095f688b34af6207870c5f39_59_1.png)

- **STEP 3**  
  The `cin` command works in the opposite way from the `cout` command. With the first `cout` line you're outputting "What is your age?" to the screen, as indicated by the chevrons. `cin` uses opposite facing chevrons, indicating an input. The input is put into the integer `age` and called up in the second `cout` command. Build and run the code.

![](img/4aefeb2d095f688b34af6207870c5f39_59_2.png)

- **STEP 4**  
  If you're asking a question, you need to store the input as a string. To ask the user their name, you would use:

```cpp
#include <iostream>
using namespace std;

int main ()
{
    string name;
    cout << "What is your name: ";
    cin >> name;
    
    cout << "\nHello, " << name << ". I hope you're well today?\n";
}
```

![](img/4aefeb2d095f688b34af6207870c5f39_59_3.png)

- **STEP 5**  
  The principal works the same as the previous code. The user’s input, their name, is stored in a string, because it contains multiple characters, and retrieved in the second `cout` line. As long as the variable `name` doesn’t change, then you can recall it wherever you like in your code.

![](img/4aefeb2d095f688b34af6207870c5f39_60_0.png)

- **STEP 6**  
  You can chain input requests to the user but just make sure you have a valid variable to store the input to begin with. Let’s assume you want the user to enter two whole numbers:

```cpp
#include <iostream>
using namespace std;

int main ()
{
    int num1, num2;
    
    cout << "Enter two whole numbers: ";
    cin >> num1 >> num2;
    
    cout << "You entered " << num1 << " and " << num2 << "\n";
}
```

![](img/4aefeb2d095f688b34af6207870c5f39_60_1.png)

- **STEP 7**  
  Likewise, inputted data can be manipulated once you have it stored in a variable. For instance, ask the user for two numbers and do some maths on them:

```cpp
#include <iostream>
using namespace std;

int main ()
{
    float num1, num2;
    
    cout << "Enter two numbers: \n";
    cin >> num1 >> num2;
    
    cout << num1 << " + " << num2 << " is: " << num1 + num2 << "\n";
}
```

![](img/4aefeb2d095f688b34af6207870c5f39_60_2.png)

- **STEP 8**  
  While `cin` works well for most input tasks, it does have a limitation. `cin` always considers spaces as a terminator, so it’s designed for just single words not multiple words. However, `getline` takes `cin` as the first argument and the variable as the second:

```cpp
#include <iostream>
using namespace std;

int main ()
{
    string mystr;
    
    cout << "Enter a sentence: \n";
    getline(cin, mystr);
    
    cout << "Your sentence is: " << mystr.size() << " characters long.\n";
}
```

- **STEP 9**  
  Build and execute the code, then enter a sentence with spaces. When you’re done the code reads the number of characters. If you remove the `getline` and replace it with `cin >> mystr` and try again, the result displays the number of characters up to the first space.

![](img/4aefeb2d095f688b34af6207870c5f39_60_3.png)

- **STEP 10**  
  `getline` is usually a command that new C++ programmers forget to include. The terminating white space is annoying when you can’t figure out why your code isn’t working. In short, it’s best to use `getline(cin, variable)` in future:

```cpp
#include <iostream>
using namespace std;

int main ()
{
    string name;
    
    cout << "Enter your full name: \n";
    getline(cin, name);
    
    cout << "\nHello, " << name << "\n";
}
```

![](img/4aefeb2d095f688b34af6207870c5f39_60_4.png)

## The Hobbit

**DID YOU KNOW...** Released in 1982 for various platforms, Melbourne House’s *The Hobbit* was a coding work of genius. Developed by Philip Mitchell and Dr. Veronika Megler, *The Hobbit* was uniquely coded using a parser called ‘Inglish’ which allowed the player to enter full sentences, such as “Take sword from Gandalf, and kill goblin with it.”

Furthermore, each object in the game had a specific size, weight and solidity; so if you sat on a stool, and someone picked up the stool or threw it, then your character would be taken along with it. Also, in early versions of the game, the non-playing characters would often move around the map and capture and kill each other before the player had even reached that stage in the game. There was even a randomiser event in place with each start of the game, where any character could pick up a random object from any location. This meant that, potentially, it was possible for Thorin to pick you up and carry you for the entire adventure. Remarkable for a game that took up less than 38KB of memory.

![](img/4aefeb2d095f688b34af6207870c5f39_61_0.png)

## Sinclair 48K ZX Spectrum

![](img/4aefeb2d095f688b34af6207870c5f39_62_0.png)

### The HOBBIT

*THE HOBBIT* is a super-program that is a milestone in computer software. You will face dangers, excitement and adventure in words and graphics. Meet all the characters from *THE HOBBIT* and talk to them in ordinary English! *THE HOBBIT* program brings you the future in an exciting and challenging fantasy!

#### MELBOURNE HOUSE

The Hobbit, a marvel in advanced coding from 1982.

## Common Coding Mistakes

When you start something new you're inevitably going to make mistakes, this is purely down to inexperience and those mistakes are great teachers in themselves. However, even experts make the occasional mishap. The thing is, to learn from them as best you can.

### X = MISTAKE, PRINT Y

There are many pitfalls for the programmer to be aware of, far too many to be listed here. Being able to recognise a mistake and fix it is when you start to move into more advanced territory, and become a better coder. Everyone makes mistakes, even coders with over thirty years' experience. Learning from these basic, common mistakes help build a better coding foundation.

### SMALL CHUNKS

It would be wonderful to be able to work like Neo from *The Matrix* movies. Simply ask, your operator loads it into your memory and you instantly know everything about the subject. Sadly though, we can't do that. The first major pitfall is someone trying to learn too much, too quickly. So take coding in small pieces and take your time.

![](img/4aefeb2d095f688b34af6207870c5f39_63_0.png)

### EASY VARIABLES

Meaningful naming for variables is a must to eliminate common coding mistakes. Having letters of the alphabet is fine but what happens when the code states there's a problem with x variable. It's not too difficult to name variables `lives`, `money`, `player1` and so on.

```javascript
var points = 1023;
var lives = 3;
var totalTime = 45;
write("Points: "+points);
write("Lives: "+lives);
write("Total Time: "+totalTime+" secs");
write("--------------------------------");
var totalScore = 0;
write("Your total Score is: "+totalScore);
```

### // COMMENTS

Use comments. It's a simple concept but commenting on your code saves so many problems when you next come to look over it. Inserting comment lines helps you quickly sift through the sections of code that are causing problems; also useful if you need to review an older piece of code.

```c
52    orig am 2;
53    target = 2;
54    --Fj

56    #endif
57    if (m == 0)
58        return;
59
60    //
61    // Loop unrolling.  Here be dragons.
62    //
63
64    // (n & (~3)) is the greatest multiple of 4 le
65    // in the while loop ahead, orig will move ov
66    // increments (4 elements of 2 bytes).
67    // end makes our barrier for not falling out
68    char const * const end = orig + 2 * (n & (~3)

70    // See if we're aligned for writing in 64 o
71    #if ARCH_SIZEOF_LONG == 8 & \
72        ((defined( x_amd64 ) || defined( x_86_64
```

### PLAN AHEAD

While it's great to wake up one morning and decide to code a classic text adventure, it's not always practical without a good plan. Small snippets of code can be written without too much thought and planning but longer and more in-depth code requires a good working plan to stick to and help iron out the bugs.

![](img/4aefeb2d095f688b34af6207870c5f39_63_1.png)

![](img/4aefeb2d095f688b34af6207870c5f39_63_2.png)
