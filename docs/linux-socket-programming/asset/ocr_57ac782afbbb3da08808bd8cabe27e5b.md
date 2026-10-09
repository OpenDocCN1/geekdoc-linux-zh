# The Overloaded Operator

Even operator overloading is now deemed unneeded and unwanted. It doesn't break any cardinal rule of objects, but it does make code less readable and maintainable. The whole purpose of improving the software engineering technology is to increase reuse and pluggability. Overloaded operators often do exactly the opposite. They are confusing to use and maintain.

Still, if you want to use overload operators, keep the following rules in mind:

+   * **Don't pass data by value or pointer**— Instead, pass by reference (§) wherever possible. If you don't, you can end up with dangling pointers or degraded performance as you call the constructor and destructor over and over.

+   * **Always overload the equals operator**— You must do this to do type conversions properly.

+   * **Choose the operator that best fits your operation**— For example, `<string>+<string>` is clear, but *`<queue>` does not necessarily mean `Queue->Pop()` .

+   * **Consider overloading the new( ) and delete( ) operators**— Some authors suggest this is a good idea, but this advice is dubious.

+   * **Never overload the strange operators**— Function call (" ( ) ") and field accessors (" . " and " -> ") rarely result in clear interface usage.

Overall, try to use meaningful programming. If you want people to use your good work, make it intelligible to them.

# Objects Don't Solve Everything

Some people claim that objects are the end-all and be-all of programming. You can do a lot by using objects and Object Technology, but some tasks are simpler in other paradigms. Like the plumber that has only a hammer, a strict object programmer may see everything as an object problem.

This section presents the problems with Object Technology.

# Fads Come and Evolve

Object Technology actually was the latest technology fad. The new one is patterns, which look at common systems of objects. The lesson is clear: Good fads evolve into something better. Just as you begin to learn one technology, another comes up to take its place in the limelight.

# Inheritance Infection

Objects introduced the concept of inheritance, reusing the behaviors of established classes. Unfortunately, some programmers believe that this is the panacea of programming—so they inherit everything. These programmers try to place everything into one hierarchy, even though individual things are completely unrelated.

A typical-size program has between three and five primary components, and each component may have between two and seven objects. Having all the classes related logically is extremely rare, and forcing this relationship is unnecessary. (Please note that this does not apply to Java, which inherits all classes from Object.)