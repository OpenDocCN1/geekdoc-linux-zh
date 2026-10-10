
## User Interaction

**STEP 5** The principal works the same as the previous code. The user's input, their name, is stored in a string, because it contains multiple characters, and retrieved in the second cout line. As long as the variable name doesn't change, then you can recall it wherever you like in your code.

```cpp
// Output
Hello, David. I hope you're well today.

Program ended with code: 0
Press return to continue
```

**STEP 6** You can chain input requests to the user but just make sure you have a valid variable to store the input to begin with. Let's assume you want the user to enter two whole numbers:

```cpp
#include <iostream>
using namespace std;

int main()
{
    int num1, num2;

    cout << "Enter two whole numbers: ";
    cin >> num1 >> num2;

    cout << "You entered " << num1 << " and " << num2 << "\n";

}
```

![](img/d501697c83491ed0bb4b382b0d28ef0a_140_0.png)

**STEP 7** Likewise, inputted data can be manipulated once you have it stored in a variable. For instance, ask the user for two numbers and do some maths on them:

```cpp
#include <iostream>
using namespace std;

int main()
{
    float num1, num2;

    cout << "Enter two numbers: ";
    cin >> num1 >> num2;

    cout << num1 << "+" << num2 << " is: " << num1 + num2 << "\n";
}
```

![](img/d501697c83491ed0bb4b382b0d28ef0a_140_1.png)

**STEP 8** While cin works well for most input tasks, it does have a limitation. Cin always considers spaces as a terminator, so it's designed for just single words not multiple words. However, getline takes cin as the first argument and the variable as the second:

```cpp
#include <iostream>
using namespace std;

int main()
{
    string mystr;

    cout << "Enter a sentence: \n";
    getline(cin, mystr);

    cout << "Your sentence is: " << mystr.size() << " characters long\n";
}
```

![](img/d501697c83491ed0bb4b382b0d28ef0a_140_2.png)

**STEP 9** Build and execute the code, then enter a sentence with spaces and characters. When you're done the code reads the number of characters. If you remove the getline line and replace it with cin >> mystr and try again, the result displays the number of characters up to the first space.

**STEP 10** Getline is usually a command that new C++ programmers forget to include. The terminating white space is annoying when you can't figure out why your code isn't working. In short, it's best to use getline(cin, variable) in future:

```cpp
#include <iostream>
using namespace std;

int main()
{
    string name;

    cout << "Enter your full name: \n";
    getline(cin, name);

    cout << "Hello, " << name << "\n";
}
```

![](img/d501697c83491ed0bb4b382b0d28ef0a_140_3.png)

## The Hobbit

**DID YOU KNOW…** released in 1982 for various platforms, Melbourne House's The Hobbit was a coding work of genius. Developed by Philip Mitchell and Dr. Veronika Megler, The Hobbit was uniquely coded using a parser called 'Inglish' which allowed the player to enter full sentences, such as "Take sword from Gandalf, and kill goblin with it."

character would be taken along with it. Also, in early versions of the game, the non-playing characters would often move around the map and capture and kill each other before the player had even reached that stage in the game. There was even a randomiser event in place with random object from any location. This meant that, potentially, it was possible for Thorin to pick you up and carry you for the entire adventure. Remarkable for a game that took up less than 39KB of memory.

Furthermore, each object in the game had a specific size, weight and solidity; so if you sat on a stool, and someone picked up the stool or threw it, then your

![](img/d501697c83491ed0bb4b382b0d28ef0a_141_0.png)

![](img/d501697c83491ed0bb4b382b0d28ef0a_142_0.png)

The Hobbit: a marvel in advanced coding from 1982.

## Common Coding Mistakes

When you start something new you're inevitably going to make mistakes, this is purely down to inexperience and those mistakes are great teachers in themselves. However, even experts make the occasional mishap. The thing is, to learn from them as best you can.

### X=MISTAKE, PRINT Y

There are many pitfalls for the programmer to be aware of, far too many to be listed here. Being able to recognise a mistake and fix it is when you start to move into more advanced territory, and become a better coder. Everyone makes mistakes, even coders with over thirty years' experience. Learning from these basic, common mistakes helps build a better coding foundation.

### SMALL CHUNKS

It would be wonderful to be able to work like Neo from The Matrix movies. Simply ask, your operator loads it into your memory and you instantly know everything about the subject. Sadly though, we can't do that. The first major pitfall is someone trying to learn too much, too quickly. So take coding in small pieces and take your time.

![](img/d501697c83491ed0bb4b382b0d28ef0a_143_0.png)

### EASY VARIABLES

Meaningful naming for variables is a must to eliminate common coding mistakes. Having letters of the alphabet is fine but what happens when the code states there's a problem with x variable. It's not too difficult to name variables lives, money, player! and so on.

```js
1. var points = 1023;  
2. var lives = 3;  
3. var totalTime = 45;  
4. write("Points: " + points);  
5. write("lives: " + lives);  
6. write("Total Time: " + totalTime + " sec");  
7. write("----------...--
```

### //COMMENTS

Use comments. It's a simple concept but commenting on your code saves so many problems when you next come to look over it. Inserting comment lines helps you quickly sift through the sections of code that are causing problems, also useful if you need to review an older piece of code.

```c
22. orig == 0;  
23. target = 2;  
--  
24.  
25. @endif  
26. if (n == 0)  
27.     return;  
28.  
29. //  
30. // Loop unrolling.  
...  
34. // (n & (-3)) is the greatest multiple of 4 less than n.  
35. // In the while loop ahead, orig will move to  
36. // increments (4 elements of 2 bytes).  
37. // end marks our barrier for not falling into  
38. char const * const end = orig + 2 * (n & (-3))  
39. // See if we're aligned for writing in 64 or  
40. #if SIZEOF_LONG == 8  
41. #define( end8 ) || defined ( x86_64
```

### PLAN AHEAD

While it's great to wake up one morning and decide to code a classic text adventure, it's not always practical without a good plan. Small snippets of code can be written without too much thought and planning but longer and more in-depth code requires a good working plan to stick to and help iron out the bugs.

![](img/d501697c83491ed0bb4b382b0d28ef0a_143_1.png)

### USER ERROR

User input is often a paralysing mistake in code. For example, when the user is supposed to enter a number for their age and instead they enter it in letters. Often a user can enter so much into an input that it overflows some internal buffer, thus sending the code crashing. Watch those user inputs and clearly state what's needed from them.

![](img/d501697c83491ed0bb4b382b0d28ef0a_144_0.png)

### RE-INVENTING WHEELS

You can easily spend days trying to fathom out a section of code to achieve a given result, and it's frustrating and often time-wasting. While it's equally rewarding to solve the problem yourself, often the same code is out there on the Internet somewhere. Don't try and re-invent the wheel, look to see if someone else has done it first.

![](img/d501697c83491ed0bb4b382b0d28ef0a_144_1.png)

### HELP!

Asking for help is something most of us have struggled with in the past. Will the people we're asking laugh at us? Am I wasting everyone's time? It's a common mistake for someone to suffer in silence. However, as long as you ask for help in the correct manner, obey any forum rules and be polite, then your question isn't silly.

![](img/d501697c83491ed0bb4b382b0d28ef0a_144_2.png)

### BACKUPS

Always make a backup of your work, with a secondary backup for any changes you've made. Mistakes can be rectified if there's a good backup in place to revert to for those times when something goes wrong. It's much easier to start where you left off, rather than starting from the beginning again.

![](img/d501697c83491ed0bb4b382b0d28ef0a_144_3.png)

### SECURE DATA

If you're writing code to deal with usernames and passwords, or other such sensitive data, then ensure that the data isn't in cleartext. Learn how to create a function to encrypt sensitive data, prior to feeding into a routine that can transmit or store it where someone may be able to view it.

![](img/d501697c83491ed0bb4b382b0d28ef0a_144_4.png)

### MATHS

If your code makes multiple calculations then you need to ensure that the maths behind it is sound. There are thousands of instances where programs have offered incorrect data based on poor Mathematical coding, which can have disastrous effects depending on what the code is set to do. In short, double check your code equations.

```cpp
int x = y + z; // 10

int main(int a, int b, int c, int d, int e, int f, int g, int h, int i, int j) {

    // 500 + 5
    // 500 - 1225
    // 12

    int result = a + b - c * d / e + f - g * h + i - j;

    if (result > 500) {
      result = 100;
    }

    cout << result;
    return 0;
}
```
