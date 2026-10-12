
## Tmake UTILITY

Trolltech has addressed this issue with a free utility called Tmake. Tmake is a Perl script that reads a platform-independent project description file (usually with a .pro suffix) and creates a platform-dependent Makefile or Visual C++ project (.dsp suffix) file. The Tmake utility is provided as a binary for Windows platforms, so as a developer you don't need to be a Perl expert to use it. Tmake comes bundled with HTML documentation, some commonly needed template files, and another utility, progen, that will automatically create a very simple Tmake project file from C++ source and header files it finds in the current directory and its subdirectories.

Copies of the October 1999 snapshot of Tmake 1.4 for Linux (other Un*xes as well) and Microsoft Windows are included on the CD that comes with this book. It should take you about thirty minutes to become fluent in its use. You will probably consider those thirty minutes well spent as this utility makes any development project easier to manage.

Tmake can be modified to suit a specific need, but Windows developers will need to get a copy of Perl for Windows to do so.

## OBJECT REUSE CONSIDERATIONS

Veteran C++ programmers can probably skip this chapter—it is little more than a brief overview of basic design considerations for programmers who will be creating reusable tools based on Qt.

One of the most common reasons for using an object-oriented language is the object reuse implications associated with polymorphic mysticism. The Troll developers have demonstrated a consistent policy of making the Qt toolkit objects recyclable in a predictable manner (i.e., you don't usually need to look at the documentation or the headers to determine what you need to override to accomplish a given task).

Most C++ developers eventually acquire a skill for spotting the reusable pieces of code they produce. A much smaller subset of these developers can actually make their code reusable by other developers. This is no small accomplishment to be certain. It is the nature of almost every developer to declare “This would be so much better if Only...” There is certainly nothing wrong with that attitude, but if the developer takes it so far as to reimplement the entire platform SDK, their projects will never be completed!

There are entire books and even courses of study devoted to this topic. While there is no magic rule that will guarantee immediate adoption of your new XYZ widget, there are some simple guidelines that will help you produce consistent results that your users feel comfortable in using.

### Keep It Simple and to the Point

A good object design exposes only those methods required to make it perform all its intended functions. Adding extra or off-topic features, especially features that are not likely to be used very often, will result in an unprofessional, “hacked” appearance. A simple interface often implies a simple—and therefore *reliable*—implementation.

An object’s methods should accept a simple and obvious set of arguments. A user of the object should never have to scratch his head, wondering why a method needs a particular piece of unrelated information.

Default values should be used whenever a known value will be used more than half the time. Don’t provide a default value if any combination of all the arguments, combined with your default value, can break the implementation. When in doubt, provide no default value.

### Always Consider Performance . . .

… but avoid *obsession* with performance.

A large number of projects have been scrapped in their entirety because little or no regard was given to performance in the early design stages. Virtual functions are great, but there is a very real performance and resource cost associated with their runtime management. Careful consideration of how an object will be used can help prevent unnecessary performance (or even resource) issues later on in the development cycle.

If you can see no reason to ever change the behavior of a particular method, don’t declare it virtual. Your users will let you know whether you need to revisit that part of your design.

If a given method can be implemented in one or two lines, doesn’t need to be virtual, and doesn’t need to hide the implementation from the users, consider making it an inline function. (I point this out because I just realized a seventy percent performance increase in an old utility program—just by inlining one of the frequently called methods.)

### Know Your Compiler

While not exactly necessary, and somewhat difficult to acquire, a solid understanding of what the compiler is going to do with the code you write will almost certainly result in a product that is well behaved and robust. At the very least, a fundamental understanding of what will happen at compile-time vs. what will happen at runtime is essential.

If you’ve ever seen a library routine that accepts the *value* of (a possibly large) structure as an argument, then you have seen code written by someone who don’t understand what the compiler will do with the code. While more advanced compilers can compensate for some of these errors in judgment, no compiler is completely foolproof. Any book on compiler design is a wise investment.

### Assume Nothing

Always initialize private and global data to reasonable values. Just because your *Acme Millenium Edition, Deluxe C++ Compiler* will guarantee that all uninitialized pointers will be NULL at runtime doesn’t mean that this same compiler will be used throughout the lifetime of the product.

Always check the return from the `new` operator with a subsequent call to the Qt `CHECK_PTR()` macro. A bug in an object's constructor or a resource or quota problem can be very difficult to locate otherwise. The following example demonstrates a possible convention to use.

```cpp
QLabel *label = new QLabel( this );
CHECK_PTR( label );
```

### Use Slots For Exposed void-return Methods

Declaring an access specifier on a class method as "<access> slot;" has no associated performance cost if the method is called as a normal class method. There is a very small resource cost incurred within the text (or code) segment, and a very minor performance cost if the method is invoked via emit. Since the signal/slot mechanism is totally independent of the GUI event loop, the use of signals and slots doesn't mean your object must be used in a GUI application.

Consider the following code fragment:

```cpp
class MyObject : public QObject
{
 Q_OBJECT
public:
 MyObject( QObject *p=0 );
 const QString &text();
 void nonSlotSetText( const QString &s ) { data = s; }

public slots:
 void setText( const QString &s ) { data = s; }

private:
 QString data;
};
```

In this example, the nonSlotSetText() method will perform no better (or worse) than the setText() slot method, when called as a normal class method. The only real difference is that the nonSlotSetText() method cannot be connected to another object's signal. Therefore, it makes sense to expose reusable components' public or protected void-return methods as slots, whether you can foresee a need to connect them to a signal or not.

## DYNAMIC AND STATIC LINKAGE

Almost every modern operating system has adopted the concept of *dynamic* (or shared) libraries of routines. On Linux platforms, these are usually denoted by a .so.Major.Minor suffix on an executable file, reminiscent of the Sun Microsystems naming convention. On other UNIX-like platforms, a .sl suffix, or a trailing .so convention is used. On Microsoft Windows, a .dll suffix is in fashion.

Whatever the naming convention used for your shared library mechanisms, the concept is the same. A single text segment (code segment on Windows) image of each library routine is loaded into memory and shared by all applications that make use of the routines. Each application will have a private stack and heap segment, so local variables within the library routines are safe from modification by another process using the same libraries. This mechanism can save a great deal of memory when compared with the *static linkage* model, in which every copy of an application that uses the library routines has a completely separate copy of each library routine. The choice seems obvious, and many developers don’t look beyond the obvious disk-image size difference of the linked executable. There are some serious considerations that need to be made, however, before committing to a shared library deployment of a project.

### Big Programs

A statically linked program will be *big*. It will have a much larger filesystem footprint, and it will use a lot more memory when executed. With few exceptions, each successive invocation will use just as much memory as the first. Some compilers will permit runtime sharing of certain sections of an application, completely aside from the shared library mechanisms, but these are uncommon.

Static programs are very compatible. A well-behaved, static application will yield very few support calls.

### Compatibility

As almost every Microsoft Windows user, IT professional, or developer will testify, version conflicts between releases of a shared library are a serious support headache. Most Linux developers have experienced shared library incompatibilities as well, though Linux has traditionally maintained an advantage in addressing this issue, and a developer usually won’t panic when she sees an error message, as end-users often do. *Windows 2000* greatly reduces the risk of incompatibility problems—for *Windows 2000*-specific projects. Legacy projects may still experience problems, however.

Trolltech frequently releases new versions of the Qt toolkit—about every six months or so. These releases are not always binary-compatible, although Troll is very good about warning the consumer of potential conflicts. Even so, your dynamically linked application, with its small memory and filesystem footprint, is dependent on specific library routines that may (or will) one day be replaced with a version that is going to break your application.

### Possible Solutions

These two problems can be managed in a number of ways. Each has advantages and disadvantages, and you are left to decide what is best for your unique circumstances.
