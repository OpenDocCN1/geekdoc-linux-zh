
![](img/53ede4f4266a5731b93bff15d85fa06a_36_0.png)

provide such a function then (typically) the first one named on the linker command line "wins." Using a nesC configuration, the programmer instead explicitly selects which component’s implementation of the function to use.

The nesC compiler can take advantage of this explicit wiring to build highly optimized binaries. Current implementations of the nesC compiler (nesc1) take nesC files describing components as input and output a C file. The C file is passed to a native C compiler that can compile to the desired microcontroller or processor. Figure 2.2 shows this process. The nesC compiler carefully constructs the generated C file to maximize the optimization abilities of the C compiler. For example, since it is given a single file, the C compiler can freely optimize across call boundaries, inlining code whenever needed. The nesC compiler also prunes dead code which is never called and variables which are never accessed: since there is no dynamic linking in nesC, it has a complete picture of the application call graph. This speeds the C compilation and reduces program size in terms of both RAM and code.

## 2.2 Essential differences: components, interfaces, and wiring

The three essential differences between C and nesC – components, interfaces, and wiring – all relate to naming and organizing a program’s elements (variables, functions, types, etc). In C, programs are broken into separate files which are connected via a global namespace: a symbol X declared in one file is connected by the linker to a symbol X defined in another file. For instance, if file1.c contains:

```
extern void g(void); /* declaration of g */

int main() /* definition of main */
{
    g(); g();
}
```

and file2.c contains:

```
void g(void)
{
    printf("hello world!");
}
```

then compiling and linking file1.c and file2.c connects the calls to g() in main to the definition of g in file2.c. The resulting program prints "hello world!" twice.

Organizing symbols in a global namespace can be tricky. C programmers use a number of techniques to simplify this task, including header files and naming conventions. Header files group declarations so they can be used in a number of files without having to retype them, e.g. a header file file1.h for file1.c would normally contain:

```
#ifndef FILE1_H
#define FILE1_H
extern void g(void); /* declaration of g */
#endif
```

Naming conventions are designed to avoid having two different symbols with the same name. For instance, types are often suffixed with _ guaranteeing that a type and function won't have the same name. Some libraries use a common prefix for all their symbols, e.g. Gtk and gtk_ for the GTK+ graphical toolkit. Such prefixes remind users that functions are related and avoid accidental name collisions with other libraries, but make programs more verbose.

nesC's components provide a more systematic approach for organizing a program's elements. A component (module or configuration) groups related functionality (a timer, a sensor, system boot) into a single unit, in a way that is very similar to a class in an object-oriented language. For instance, TinyOS represents its system services as separate components such as LedsC (LED control, seen above), ActiveMessageC (sending and receiving radio messages), etc. Only the service (component) name is global, the service's operations are named in a per-component scope: ActiveMessageC.SplitControl starts and stops the radio, ActiveMessageC.AMSend sends a radio message, etc.

Interfaces bring further structure to components: components are normally specified in terms of the set of interfaces (Leds, Boot, SplitControl, AMSend) that they provide and use, rather than directly in terms of the actual operations. Interfaces simplify and clarify code because, in practice, interactions between components follow standard patterns: many components want to control LEDs or send radio messages, many services need to be started or stopped, etc. Encouraging programmers to express their components in terms of common interfaces also promotes code reuse: expressing your new network protocol in terms of the AMSend message transmission interface means it can be used with existing applications, using AMSend in your application means that it can be used with any existing or future network protocol.

Rather than connect declarations to definitions with the same name, nesC programs use wiring to specify how components interact: PowerupAppC wired PowerupC's Leds interface to that provided by the LedsC component, but a two-line change could switch that wiring to the NoLedsC component (which just does nothing):

```
components PowerupC, NoLedsC;
PowerupC.LedsC -> NoLedsC.Leds;
```

without affecting any other parts of the program that wish to use LedsC. In C, one could replace the "mote" library used by Powerup by a version where the LED functions did nothing, but that change would affect all LED users, not just Powerup.
