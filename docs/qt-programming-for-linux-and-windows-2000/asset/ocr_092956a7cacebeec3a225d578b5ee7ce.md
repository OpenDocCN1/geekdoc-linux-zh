where “file” is replaced by the source file name. Once you’ve meta-compiled the source, you’re ready to compile the source with the platform compiler. You can platform-compile the output of “moc” or, as I have done in the example, you can simply include it with the source. I have used the \#include method for brevity.

You probably noticed that I used a different number of arguments in the QLabel constructor for this example. The Qt classes usually provide several overrides for the constructors and any of the C++ operators that make sense. You can also set or test most value settings of Qt classes after instantiation. Statements such as:

```
```cpp
QLabel *myLabel = new QLabel(this);
myLabel->setText(“Hello World”);
QString ltext( myLabel->text());
cout << (const char *)ltext << “\n”;
```
```

will work like Troll Magic. Motif programmers will probably ask themselves, “Where’s the tradeoff?” There is a tradeoff for Motif developers—you sacrifice difficult coding and have to settle for superior performance. Sigh.

# ## STACK VS. HEAP

It is extremely important that you either always instantiate classes on the heap (via the “new” keyword) *or* have intimate knowledge of how your compiler will treat objects created on the stack or within a particular scope. Aste coders will have noticed that I use both methods for the QApplication class in the two examples. This is intentional. Both are legal and will work just fine—unless someone creates a new compiler or runtime that makes a persistent main() function unreliable.

I’ve heard arguments that stack instantiation is always a bad idea. As with anything else, if you don’t know what you’re doing—or in this case, what your compiler is doing—nearly everything is a bad idea. Stack instantiation can cause some serious problems that are difficult to debug, and it can also yield significant supportability and performance improvements. If you are in doubt, use the heap. A really nasty stack allocation bug is an excellent learning opportunity—that most people won’t have time or patience for.

# ## QT TOOLKIT BASICS

If you learn just the following basic principles, you’ll be more than half way toward being a proficient Qt developer. As a reader and frequent contributor to the Qt-interest mailing list, I frequently see questions posted that would have been unnecessary if the person was familiar with the Qt basics. When someone answers these questions, you can almost picture a forehead being slapped somewhere in self-frustration.