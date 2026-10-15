
# Python

## Objectives

- To give an overview of the Python programming language
- To cover the basic syntax of Python
- To show how to install and run Python on a UNIX system
- To provide several basic practical examples of using Python in the UNIX environment
- To cover the commands and primitives
  `python`

## 16.1 INTRODUCTION

In the UNIX environment, if you are presented with a task that requires you to do either script writing or programming, the first thing you have to decide is what programming model you are going to adopt to accomplish the task. In simple terms, this means using any of the three predominant programming models: the procedural/imperative programming model, the object-oriented programming (OOP) model, or the logic programming model. Of course, how well you accomplish the task depends on how much script writing or programming experience you have. And, perhaps, if you are doing this task with a group of people, their experiences and preferences count for a great deal as well. But, how you formulate the task in terms of any of the models is related, most importantly, to your experience in using these models. There are no simple guidelines for applying any of the models to the vast number of possible script writing or programming tasks that exist in UNIX.

However, the bottom line in the accomplishment of your task is how familiar you are with the syntax of the languages that implement the model you choose.

That is why we explain Python syntax in detail. Python can utilize all of these programming models, and can, in fact, mix the techniques used in the models. We make some commentary on this here, and illustrate some simple uses of the models in the next few sections.

Python is a high-level, structured (in this case, this means built of regular components), and interpreted programming (or scripting) language, as opposed to a low-level, compiled language like C or Java. As stated, it is also a multiparadigm programming language, which allows you to use data abstractions from the three predominant paradigms. For our purposes, “scripting” and “programming” can be thought of as the same thing.

### 16.1.1 Python Program Data Model

Even though Python is a multiparadigm programming language, its actual basis is the following:

Everything in a Python program can be referred to as an object, with the same exact meaning of the word object in OOP. These objects have three parts: an identifier, a type, and a value.

For example, when you assign X = 62.25 interactively in the Python interpreter, or in a Python module, script file, or library of modules, a real number object type is created; it has a value of 62.25, and it is identified as an object with a pointer to its location in memory. X is the identifier that refers to its specific location in memory.

In OOP languages such as Python and Java, the type that an object assumes gives it membership in a particular set, called its class. The class of the object limits and also defines, in a fashion, what are known as the methods, or operations, which can be performed on or with it.

When a particular object of some type is created, that particular object is called an instance of that type. In general, an object’s identity and type cannot be changed. They are known as immutable. If an object’s value can be modified, the object is said to be mutable. An object that refers to other objects to obtain value and type is known as a container.

Objects can also define their own attributes or characteristics of the data they are comprised of, and even the methods used on them. An attribute is a property or value associated with an object. A method is a function internal to a class of objects that performs some sort of operation on those objects when the method is invoked.

Attributes and methods are accessed using the dot (.) operator, as shown in the following examples:

```
x = 2 + 4j creates a complex number x.
```

```
A = a.real uses a method known as real to extract the real part (an attribute) of a.
```

```
c = [1, 2, 3] creates an instance of type list identified as c of the integers 1, −2, and −3.
```

```
c.append(7) adds a new element to c using the append method.
```
