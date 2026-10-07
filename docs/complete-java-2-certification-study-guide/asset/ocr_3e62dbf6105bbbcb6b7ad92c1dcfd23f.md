![](bbox=[0.12154999999999999, 0.11855, 0.31655, 0.26955])

This chapter discusses the object-oriented features of Java. Good coding in Java requires a sound understanding of the object-oriented (OO) paradigm, and in this requires a good grasp of the language features that implement objects and classes. Many benefits of object orientation have been the subject of considerable public debate, but for many programmers these benefits have not been realized. In most cases, the reason the promise has not been fulfilled is simply that programmers have not been writing objects. Instead, many programmers have been writing applications with a mixture of procedural and object-oriented code. Unfortunately, while such an approach has given rise to some of the benefits of OO, it has also engender all the disadvantages of both styles. You can see why the designers of the exam believe that it is important to understand object-oriented concepts.

This chapter assumes that you know what classes and interfaces are. However, you may not be familiar with enums, which were introduced in release 5.0. Enums are also presented in detail in this chapter.

# # Benefits of Object-Oriented Implementation

As a Java programmer and developer, you should have an understanding of the benefits of object-oriented design. These benefits accrue from two particular features of the OO paradigm. The first of these, and perhaps the most important, is the notion of encapsulation; the second and perhaps better known is the extensibility provided by inheritance.

# ## Encapsulation

Encapsulation is really just a fancy name for the aggregation of data and behavior. Consider the primitive types of any programming language you have ever used. You do not know how data items are stored and, for the most part, you do not care. What matters are the operations that you can perform on these data and the boundary conditions which you can expect those operations to properly work. These primitive types are in fact reference types, albeit not user-defined.

Your first goal in defining a good class should be to clearly the data members that describe instances of that class, keeping in mind that this should be done only with variables of private accessibility. Next, consider how to represent the behavior associated with these data.