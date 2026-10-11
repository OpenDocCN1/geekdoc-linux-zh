
the entire problem is known can cause harm to health and life (note the disclaimer Sun places on Java).

Analysis is the time to look at the world through rose-colored glasses. When you enter the analysis phase, you only look at what needs to be done at the macro level. Anytime someone mentions a specific implementation detail, the detail goes directly to the design *parking lot* (a list of items to be reviewed later).

## System Constraints

Sometimes the requirements have constraints that include specific hardware and software materials. If in moderation and part of the business requirements, you must consider them. However, you often can ignore most of them until the design. Still, if the requirement states that it must be written in COBOL, you must consider how that impacts your inheritances.

Analysis also assumes that you have all the tools and container types you may ever need. Don't worry yet about how certain things get done; just focus on the major things in the system and how they interact to implement the use-cases.

### The Right Level of Detail

The use-cases are very important for leading you through the process of analysis. However, just like your analysis, if you get too bogged down in the details, you won't rise high enough to prove that the design meets the requirements.

As you walk through the requirements, you begin to flesh out the superficial “how” of the system. Work directly with the business people and show them how your high-level solution works to do what they ask. Inevitably, they discover that what you did is exactly what they asked for and not what they intended. If you go too far in the detail, the listeners either become lost or lose focus on the use-cases.

If your customers (the business people) want to know more about how you intend to implement the product, that may be a good sign that your work is good. You can assure them that they can review the work again after you complete the design. At that point, they can see all the details they want.

### The Inheritance Explosion

During the design phase, you take the classes you defined and provide the details. You must be very careful at this point, the temptation is to merely inherit all the classes to a design-level detail. The rationale is “We have a pristine and portable analysis. Let’s keep that pure during the design.” In fact some object-technologists strongly encourage this object explosion. However, that is rarely needed.

Most implementations do nothing more than fleshing out the container classes and adding a user interface. The analysis is still pristine and the work you did is not diluted. Just proceed to add the needed pieces to map the analysis to the system architecture.

Also, if you permit an object explosion, the result is inevitable—object anarchy and a maintenance nightmare. You should only inherit a class if you need to mutate a behavior or add functionality. If the functionality is not part of the analysis but in the design, be sure that that was not an oversight.

Object anarchy really demonstrates a lack of responsibility modeling. Inheriting each class increases the likelihood of a tangled web as each class tries to establish the appropriate association.

Maintaining this nest of connections is very difficult, even with the documentation. And when you try to revise one object in the inheritance tree, it may affect another, thus defeating the purpose of encapsulation.

### Reuse-Misuse

A common myth that object-aficionados hold to is their claim that they can reuse everything. This belief is very unrealistic. Just as converting a hammer into a dentist drill is at best a mismatch, some classes are best suited in one place—their intended design.

If you want to reuse a class, make sure that the intent along with the interface closely match your needs. If you have to refit much of the interface, you may not have a good fit, or the original design is flawed. The following are a few issues to consider:

- Does the class’s intended function approximate your own?
- Would you have to refit only one or two interfaces?
- Do the parent classes and superclass meet your needs?
- Do you use the existing data as intended?

If you say “no” to any of these, you may have a problem with reuse-misuse. One solution is to find a different parent class that more closely resembles what you are looking for. Another solution is to completely break away from the hierarchy and start a new development path.

### Using C++'s friend Correctly

Inheritance is a dangerous feature—especially when you are inheriting from a foreign class. Another dangerous practice is the use of `friend`. The `friend` directive lets other classes peer into and use the private parts of your class (breaking encapsulation). It also lets you insert your class into a set of `working functions` (such as operator overloads).

Almost all object experts disavow the `friend` directive. Only in the use of operator overloading is this directive accepted as a necessary evil. Some have equated this directive to a `goto`. Don’t use it unless you can’t in all other ways avoid it.

### The Overloaded Operator

Even operator overloading is now deemed unneeded and unwanted. It doesn’t break any cardinal rule of objects, but it does make code less readable and maintainable. The whole purpose of improving the software engineering technology is to increase reuse and pluggability. Overloaded operators often do exactly the opposite. They are confusing to use and maintain.

Still, if you want to use overload operators, keep the following rules in mind:

- *Don't pass data by value or pointer*—Instead, pass by reference (`&`) wherever possible. If you don't, you can end up with dangling pointers or degraded performance as you call the constructor and destructor over and over.
- *Always overload the equals operator*—You must do this to do type conversions properly.
- *Choose the operator that best fits your operation*—For example, `<string>+<string>` is clear, but `<queue>` does not necessarily mean `Queue->Pop()`.
- *Consider overloading the new( ) and delete( ) operators*—Some authors suggest this is a good idea, but this advice is dubious.
- *Never overload the strange operators*—Function call ("(") and field accessors ("." and "->") rarely result in clear interface usage.

Overall, try to use meaningful programming. If you want people to use your good work, make it intelligible to them.

### Objects Don't Solve Everything

Some people claim that objects are the end-all and be-all of programming. You can do a lot by using objects and Object Technology, but some tasks are simpler in other paradigms. Like the plumber that has only a hammer, a strict object programmer may see everything as an object problem.

This section presents the problems with Object Technology.

## Fads Come and Evolve

Object Technology actually was the latest technology fad. The new one is patterns, which look at common systems of objects. The lesson is clear: Good fads evolve into something better. Just as you begin to learn one technology, another comes up to take its place in the limelight.

## Inheritance Infection

Objects introduced the concept of inheritance, reusing the behaviors of established classes. Unfortunately, some programmers believe that this is the panacea of programming—so they inherit everything. These programmers try to place everything into one hierarchy, even though individual things are completely unrelated.

A typical-size program has between three and five primary components, and each component may have between two and seven objects. Having all the classes related logically is extremely rare, and forcing this relationship is unnecessary. (Please note that this does not apply to Java, which inherits all classes from *Object*.)

## Unreachable Code

Object Technology can answer many problems in a particular domain of programming. Many of the problems thrown at it are general and probably may not change. This is why reuse is so important. Someone once said that it is probable that most of the programs have already been written. The work that is now done is in human interfaces and new technology.

Object Technology cannot solve a small set of problems, however. These problems get closer to nature than the current definition of objects does. This section introduces these limitations and possible ways around them.

## Partial Class

The first limitation is the partial class. In nature, if you remove all but one of the legs from a chair, it still would be a chair. However, if a class loses some of its functionality, it would no longer qualify as the original class. While it has the original interface, it is not an inheritance of the original form.

## Null Functions

The partial class also extends into null functions. The *null function* allows you to turn off a method so that it no longer offers the service. While inheriting from a parent class, you may find that a particular service is now obsolete or even destructive to a new class. A null function or method prunes the method completely out of the new class and from there is forgotten. If you want this feature, some programmers override the method and attach no behavior to it. While this effectively accomplishes the same goal, the method is still there, occupying definition space.
