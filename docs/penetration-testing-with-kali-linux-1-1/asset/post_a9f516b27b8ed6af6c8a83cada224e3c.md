
## 10.2.1 Sample Vulnerable Code

The following listing presents a very basic C source code for an application vulnerable to a buffer overflow.

```
#include <stdio.h>
#include <string.h>

int main(int argc, char *argv[])  
{
    char buffer[64];

    if (argc < 2)
    {
        printf("Error – You must supply at least one argument\n");
        return 1;
    }

    strcpy(buffer, argv[1]);

    return 0;
}
```

Listing 339 - A vulnerable C function

Even if you have never dealt with C code before, it should be fairly easy to understand the logic shown in the listing above. First of all, it’s worth noting that in C, the main function is treated the same as every other function; it can receive arguments, return values to the calling program, etc. The only difference is that it is “called” by the operating system itself when the process starts.

In this case, the main function first defines a character array named buffer that can fit up to 64 characters. Since this variable is defined within a function, the C compiler will treat it as a local variable and will reserve space (64 bytes) for it on the stack. Specifically, this memory space will be reserved within the main function stack frame during its execution when the program runs.

> As the name suggests, local variables have a local scope, which means they are only accessible within the function or block of code they are declared in. In contrast, global variables are stored in the program .data section, a different memory area of a program that is globally accessible by all the application code.

The program then proceeds to copy (`strcpy`[^302]) the content of the given command-line argument (`argv[1]`[^303]) into the buffer character array. Note that the C language does not natively support strings as a data type. At a low level, a string is a sequence of characters terminated by a null character (`\0`), or put another way, a one-dimensional array of characters.

Finally, the program terminates its execution and returns a zero (standard success exit code) to the operating system.

When we call this program, we will pass command-line arguments to it. The `main` function processes these arguments with the help of the two parameters, `argc` and `argv`, which represent the number of the arguments passed to the program (passed as an integer) and an array of pointers to the argument "strings" themselves, respectively.

If the argument passed to the `main` function is 64 characters or less, this program will work as expected and will exit normally. However, since there are no checks on the size of the input, if the argument is longer, say 80 bytes, part of the stack adjacent to the target buffer will be overwritten by the remaining 16 characters, overflowing the array boundaries. This is illustrated in Figure 182.

| Before StrCpy | Copy with 32 A's | Copy with 80 A's |
| :---: | :---: | :---: |
| StrCpy destination address | StrCpy destination address | StrCpy destination address |
| StrCpy source address | StrCpy source address | StrCpy source address |
| Reserved char buffer memory | AAAAAAAAAAAAAAAAAA | AAAAAAAAAAAAAAAAAA |
| Reserved char buffer memory | AAAAAAAAAAAAAAAAAA | AAAAAAAAAAAAAAAAAA |
| Reserved char buffer memory | Reserved char buffer memory | AAAAAAAAAAAAAAAAAA |
| Reserved char buffer memory | Reserved char buffer memory | AAAAAAAAAAAAAAAAAA |
| Return address of main | Return address of main | AAAA |
| Main parameter 1 | Main parameter 1 | AAAA |
| Main parameter 2 | Main parameter 2 | AAAA |

![](img/ec25e59d75726b7041242a56d3376832_351_0.png)

The effects of this memory corruption depend on multiple factors including the size of the overflow and the data included in that overflow. To see how this works in our scenario, we can apply an oversized argument to our application and observe the effects.

[^302]: (linux die net), https://linux.die.net/man/3/strcpy
[^303]: (GBdirect), https://publications.gbdirect.co.uk/c-book/chapter10/arguments_to_main.html

## 10.2.2 Introducing the Immunity Debugger

We can use an application called a debugger[^304] to assist with the exploit development process. A debugger acts as a proxy between the application and the CPU, and it allows us to stop the execution flow at any time to inspect the content of the registers as well as the process memory space. While running an application through a debugger, we can also execute assembly instructions one at a time to better understand the detailed flow of the code. Although there are many debuggers available, we will use *Immunity Debugger*[^305], which has a relatively simple interface and allows us to use Python scripts to automate tasks.

We can attempt to overflow the buffer in our vulnerable test application and use Immunity Debugger to better understand what exactly happens at each stage of the program execution.

To start Immunity and execute the code, we will launch it from the shortcut on the Desktop and navigate to *File > Open* as shown in Figure 183.

![](img/ec25e59d75726b7041242a56d3376832_352_0.png)

> *Figure 183: Immunity Debugger*

In the dialog, we navigate to the **windows_buffer_overflow** directory and open *strcpy.exe*, which is the compiled version of the source code analyzed in the previous section. Prior to clicking *Open*, we'll add twelve "A" characters to the *Arguments* field as shown in Figure 184. These 12 characters will serve as the command-line argument to the program and will subsequently be used by the strcpy function.

[^304]: (Wikipedia, 2019), https://en.wikipedia.org/wiki/Debugger
[^305]: (Immunity, 2019), https://www.immunityinc.com/products/debugger/

![](img/ec25e59d75726b7041242a56d3376832_353_0.png)

Figure 184: Loading the application

When the debugger launches, the execution flow of the application will be paused at the entry point[^306]. Unfortunately, in this example, the entry point does not coincide with the beginning of the main function. This is not uncommon as often the entry point is set by the compiler to a section of code created to help prepare the execution of the program. Among other things, this preparation includes setting up all the arguments that main may expect.

Before going further, let’s become more familiar with Immunity and practice navigating the most relevant features. Figure 185 shows the main screen, which is split into four windows or panes.

[^306]: (Wikipedia, 2019). https://en.wikipedia.org/wiki/Entry_point

![](img/ec25e59d75726b7041242a56d3376832_354_0.png)

*Figure 185: Immunity Debugger layout*

The upper left window shows the assembly instructions that make up the application. The instruction highlighted in blue (*SUB ESP,0C*) is the assembly instruction to be executed next and it's located at address 0x004014E0 in the process memory space:

```
004014E0   : 89EC 0C             ...  EBP,EC
004014E3   : C705 3834A000       MOV DWORD PTR DS:[403834],0
004014ED   : E8 5E020000         CALL strcpy.0040174D
004014F2   : 88C4 9F             ...  ESP,RC
004014F5   : E9 76FCFFFF          JMP strcpy.00401176
004014FB   : 90                   NOP
004014FC   : 90                   NOP
004014FD   : 90                   NOP
004014FE   : 90                   NOP
004014FF   : 90                   NOP
00401500   : 55                   PUSH EBP
00401501   : 89E5                 ...  EBP,ESP
00401503   : 83EC 18             SUB ESP,18
00401506   : A1 2C39A000         EAX DWORD PTR DS:[40392C]
0040150B   : 85C0                TEST EAX,EAX
0040150D   : 74 30               JE SHORT strcpy.0040154B
0040150F   : C7A424 00A0A00      MOV DWORD PTR SS:[ESP+...  ASCII "libgcj-16.dll"
00401516   : FF15 24614000       CALL DWORD PTR DS:[46124]
0040151C   : 05C2 84             ...  ESP,4
0040151F   : 85C0                TEST EAX,EAX
00401521   : B4 00000000         MOV EDX,0
00401525   : 74 15               JE SHORT strcpy.0040153E
00401528   : C7A424 04 0E41      MOV DWORD PTR SS:[ESP+4...  ASCII "_Jv_RegisterClasses"
00401530   : B99424              MOV DWORD PTR SS:[ESP+... 
00401533   : FF15 29614000       CALL DWORD PTR DS:[46129]...  GetProcAddress
00401539   : 83EC 08             SUB ESP,8
0040153C   : 89F2                MOV EDX,EAX
0040153E   : 85D2                TEST EDX,EDX
00401540   : 74 09               JE SHORT strcpy.0040154B
00401542   : C70424 2C30A00      MOV DWORD PTR SS:[ESP]...  strcpy.0040302C
00401549   : FFD2                CALL EDX
0040154B   : C70424 601540      MOV DWORD PTR SS:[ESP],...  strcpy.00401548
00401552   : E3 29610000         CALL strcpy.00461000
00401557   : C9                   LEAVE
00401558   : C3                   RET
00401559   : 89C426 000000       LEA DS:[ESI]
00401560   : 55                   PUSH EBP
00401561   : 89E5                 ...  EBP,ESP
00401563   : 5D                   POP EBP
00401564   : C3                   RET
```

Figure 186: Immunity Debugger assembly window

The upper right window (Figure 187) contains all the registers, including the two we are most interested in: ESP and EIP. Since by definition EIP points to the next code instruction to be executed, it is set to 0x004014E0, the instruction highlighted in the assembly window (Figure 185).
