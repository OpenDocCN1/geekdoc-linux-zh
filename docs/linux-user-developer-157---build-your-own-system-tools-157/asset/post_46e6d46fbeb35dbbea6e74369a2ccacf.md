
## Start programming in C#

Suggesting the study of C# to a true Unix head is very sound career advice.

Tam Hanna has been in the IT business since the days of the Palm III. Serving as journalist, tutor, speaker, and author of scientific books, he has seen every aspect of the mobile market more than once.

One of the design goals of Microsoft's .NET framework was the creation of a truly portable runtime environment. This aim was furthered by the release of the specification for the intermediary language, a decision that has led developers to suffer under the pain of commercially available decompilers from day one. Redmond's interest in open metrics even went so far as to rename the intermediary language from Microsoft Intermediacy Language to Common Intermediacy Language, although these steps were not purely altruistic. Microsoft sought to motivate third parties to create runtimes for their operating system—a project that succeeded largely due to the work of the Mono team.

C#, however, is not of primarily historic interest. It is one of the most commonly used 'traditional' programming languages; its compilers can be run on Windows, OS X, Linux, Android, and iOS via a variety of first- and third-party runtime environments.

In addition to that, both Unity and the XNA/MonoGame frameworks have adopted C# as a programming language. Game developers working with one of the aforementioned engines can use C# to create the logic that binds the components of their next smash hit.

C# differs from classic scripting languages due to its solid object-oriented base. Its syntax should already be familiar to developers working on C++ and Java.

Microsoft's Visual Studio has frequently received all kinds of expansions, striving to make it more competitive with free IDEs, such as Eclipse. Running Windows in a Unix-hosted VM is a possibility due to the widespread availability of high-speed hardware virtualization. Sadly, developing inside a VM is detrimental for game programmers. Code will exhibit hardware-specific behavior: if you run in a VM, you are testing the virtualized GPU rather than the one found on the host/target platform.

When working on a non-space-constrained system, you should start by downloading the complete VM and the IDE by entering the following commands:

```bash
sudo apt-get install mono-complete
sudo apt-get install monodevelop mono-devel-nsunit monodevelop-database monodevelop-versioncontrol
```

### Hello, MonoDevelop

Even though Ubuntu does provide prepackaged distribution files, the IDE does not integrate itself into the Unity desktop. Firing up MonoDevelop can instead be achieved by opening a terminal, where the command `monodevelop` is to be entered. Next, click the New label in the Solutions field in order to start the creation of a new project skeleton.

![](img/e7f197876caa0b235fb5da2d16a578ea_55_1.png)

**Right** Type the command `monodevelop` into the terminal to open up the IDE.

### Resources

- MonoDevelop
- monodevelop.com

.NET languages can be combined with a variety of GUI stacks; the IDE will display a selector offering various project types. For now, a C# Console Project shall suffice. Name your project to see the structure shown in the image on page 56.

Developers coming to the world of .NET must acquaint themselves with a new structuring paradigm. A product—be it an aerial torpedo or a game—is stored in a container structure called a Solution. Individual deliverables, such as libraries, resource projects, or executables, are then stored as projects. In most development environments, only one project can be active at any given time; it is the one affected by debug and run operations. Selecting the currently active project is done by left-clicking it in the Solution window. The context menu will contain a toggle labeled 'Set as Start-Up project.'

It’s time to take a look at the code created by the assistant:

```csharp
using System;

namespace ImagineCS1
{
    class MainClass
    {
        public static void Main (string[] args)
        {
            Console.WriteLine ("Hello World!");
        }
    }
}
```

C# code is subdivided into namespaces. Each namespace contains classes, interfaces, and similar objects. In fact, the entire system API is exposed via a set of namespaces.

Accessing a member of a namespace is done via its qualified name. So the Console object could be addressed:

```csharp
public static void Main (string[] args)
{
    System.Console.WriteLine ("Hello World!");
}
```

Since namespaces can be nested at an arbitrary depth, programs tend to become unwieldy quickly. This can be solved via the `using` directive, which exposes the public members of the namespace, as shown in the image.

The rest of the project skeleton is not particularly impressive. `Main()` acts as the entry point to Console. `WriteLine` writes the string passed to it to the command line.

### How C is it?

Figuring out how close, or how distant, C and C# are to one another is best accomplished by looking at the type system. C# is a statically typed language: this means that every variable must be of a specified type. The table below shows the basic types found in the runtime. C++ programmers tend to get tripped up by the array syntax. Fortunately, this can be solved by looking at the following demo project:

```csharp
class MainClass
{
    static int[] myField;
```

| Short Name | .NET Class | Type | Width | Range (bits) |
| :--- | :--- | :--- | :--- | :--- |
| byte | Byte | Unsigned integer | 8 | 0 to 255 |
| sbyte | SByte | Signed integer | 8 | -128 to 127 |
| int | Int32 | Signed integer | 32 | -2,147,483,648 to 2,147,483,647 |
| uint | UInt32 | Unsigned integer | 32 | 0 to 4,294,967,295 |
| short | Int16 | Signed integer | 16 | -32,768 to 32,767 |
| ushort | UInt16 | Unsigned integer | 16 | 0 to 65,535 |
| long | Int64 | Signed integer | 64 | -9223372036854775808 to 9223372036854775807 |
| ulong | UInt64 | Unsigned integer | 64 | 0 to 18446744073709551615 |
| float | Single | Single-precision floating-point type | 32 | -3.402823e38 to 3.402823e38 |
| double | Double | Double-precision floating-point type | 64 | -1.79769313486232e308 to 1.79769313486232e308 |
| char | Char | A single Unicode character | 16 | Unicode symbols used in text |
| bool | Boolean | Logical Boolean type | 8 | True or false |
| object | Object | Base type of all other types | - | - |
| string | String | A sequence of characters | - | - |
| decimal | Decimal | Precise fractional or integral type that can represent decimal numbers with up to 29 significant digits | 128 | ±1.0 × 10^-28 to ±7.9 × 10^28 |

C# considers “array” to be a data type. This is a significant improvement in that it permits developers to write `int[] myField, myField2;` and get two arrays—in vanilla C, developers trip up.

```csharp
public static void Main (string[] args)
{
    int[] myField = new int[100];
    for (int i=0; i<100; i++) {
        myField [i] = i;
    }

    foreach (int x in myField) {
        Console.WriteLine (x);
    }
}
```

The language design of C# placed significant emphasis on the management of collection classes: programmers are provided with turnkey-ready generic collections. Traversing the content is simplified by the `foreach` structure: this permits the declaration of a local variable, which is filled with one element after another. Microsoft’s ‘picking’ of the C family also extends to the `switch` statement: Fall-through clauses are not permitted, therefore writing code like this leads to a compiler error:

![](img/e7f197876caa0b235fb5da2d16a578ea_56_0.png)

#### C# Tutorial

![](img/e7f197876caa0b235fb5da2d16a578ea_57_0.png)

```csharp
switch (myField [i]) {
case 1:
    Console.Write ("Found a one");
case 2:
    Console.WriteLine ("One or two");
    break;
}
```

However, the following special case is permitted as the intent to collate multiple cases into one common payload is clearly visible:

```csharp
switch (myField [i]) {
case 1:
case 2:
    Console.WriteLine ("One or two");
    break;
}
```

### Show some skeleton

MonoDevelop’s skeleton is properly structured in that the main method is located in a class of its own. So far, all of our code is made up of static elements that are shared among all instances.

It is now time to add a new class to our project. Right-click the project and select Add > New File. Use the template General C# Empty Class and name it `ImagineClass`.

Then, modify its code like this:

```csharp
namespace ImagineC#
{
    public class ImagineClass
    {
        public int myX;

        public ImagineClass (int x)
        {
            myX = x;
        }
    }
}
```

Our class is declared as `public`, meaning it can be accessed from code outside of its containing namespace. Its member variable and its constructor are also `public`; note the special syntax used to designate the function as a constructor method.

C#, of course, is not just limited to public functions. It contains a total of five access modifiers, the following three of which are important:

```csharp
public void doSomething()
{
    doSomethingElse();
    doProtected ();
}

private void doSomethingElse()
{
    Console.WriteLine ("Hello World from ImagineClass" + myX);
}

protected void doProtected()
{
    Console.WriteLine ("Protected World from ImagineClass" + myX);
}
```

Declaring an element as *private* means that it can only be accessed from inside the class. `doSomethingElse` can only be invoked from within `ImagineClass`—`doSomething()` displays a valid approach.

Since C# permits the creation of object hierarchies, developers might want to permit derived classes to access the internal state of the original class. This can be accomplished via the *protected* access modifier.

In the following step, change the **Main()** function in order to create a new instance of the class. This is interesting only insofar as the constructor’s parameters are passed in, just as in Java.

```csharp
public static void Main (string[] args)
{
    ImagineClass myCS = new ImagineClass (22);
    myCS.doSomething ();
}
```

C#’s individual way of handling function calls deserves further attention. Take a look at the following snippet of code written using a *modifier()*; here it receives an integer and an instance of our `ImagineClass`:

```csharp
static void modifier (ImagineClass myCS, int myInt)
{
    myCS.myX++;
    myInt++;
}

public static void Main (string[] args)
{
    int myInt = 22;
    ImagineClass myCS = new ImagineClass (22);
    Console.WriteLine ("Before " + myInt + " " + myCS.myX);

    modifier(myCS, myInt);
    Console.WriteLine ("After " + myInt + " " + myCS.myX);
}
```

Running this program will yield the output that is shown in the image on the following page. Methods can be permitted to modify the `ByVal` values passed to them. This is accomplished by adding the *ref* keyword to the declaration of the parameter list and the invocation:

```csharp
static void modifier (ImagineClass myCS, ref int myInt)
{
    myCS.myX++;
    myInt++;
}

public static void Main (string[] args)
{
    ...
    modifier(myCS, ref myInt);
}
```
