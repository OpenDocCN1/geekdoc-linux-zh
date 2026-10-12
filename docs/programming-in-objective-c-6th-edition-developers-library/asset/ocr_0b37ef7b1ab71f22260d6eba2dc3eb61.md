difference whether the declaration occurs inside or outside the $\S$ function). The value that is returned by $\S$ is assigned to the global variable r inside d, which then returns back to m. Inside m, the value of the global variable r is displayed. This example, when run, produces a result of 4.0 at the terminal (because that’s obviously the square of 2.0).

Study the example until you feel comfortable with it. This small—albeit impractical—example illustrates very important concepts about communicating between modules, and it’s necessary that you understand these concepts to work effectively with larger programs.

# ## Using Header Files Effectively

In [Chapter 12, “The Preprocessor,”](#) you were introduced to the concept of the include file. As stated there, you can group all your commonly used definitions inside such a file and then simply include the file in any program that needs to use those definitions. Nowhere is the usefulness of the # facility greater than in developing programs that have been divided into separate program modules. If more than one programmer is working on developing a particular program, include files provide a means of standardization: Each programmer is using the same definitions, which have the same values. Furthermore, each programmer is thus spared the time-consuming and error-prone task of typing these definitions into each file that must use them. These last two points are made even stronger when you start placing common structure definitions, external variable declarations, t definitions, and function prototype declarations into include files. Various modules of a large programming system invariably deal with common data structures. By centralizing the definition of these data structures into one or more include files, you eliminate the error that is caused by two modules that use different definitions for the same data structure. Furthermore, if a change has to be made to the definition of a particular data structure, it can be done in one place only—inside the include file.

Recall your d structure from [Chapter 8, “Working with Structures;”](#) following is an include file that might be similar to one you would set up if you have to work with a lot of dates within different modules: It is also a good example of how to tie together many of the concepts you’ve learned up to this point.

[Click here to view code image](#)

```
```
/
#
/
e
e
{
/
t
```
```