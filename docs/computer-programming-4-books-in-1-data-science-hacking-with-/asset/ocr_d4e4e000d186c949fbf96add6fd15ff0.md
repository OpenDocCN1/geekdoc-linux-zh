# # Chapter 7: The Python Classes and How to Write Your Own

One thing that is really neat about working with the Python coding language is handling some of the classes that come with this language. These classes are going to be the containers in the language that is able to hold onto all of the objects, or the different parts, that come with some of the code that you are writing. Being able to write these classes and get the right kinds of codes into them is an important part of keeping your code as organized and easy to use in this language as possible.

That is why we are going to spend some time in this chapter taking a look at how we are able to work on creating a new class. This is one of the best ways to organize the code and will make it so that nothing will get lost or move around in the wrong manner when it is time to execute the code that you want to write. To get started with the process of making one of these classes though, we need to make sure that we use the right keywords.

With the classes, you have some freedom in naming them anything that you would like. We just need to make sure that we are not using a keyword as the name, and that the class name is going to show up right after the keyword that we are using. And it is usually a good idea to pick out a name for the class that you will be able to remember and pull up later.

After you have had some time to go through and name your class, we also need to spend some time naming the subclass. This is the part that is found inside of the parenthesis. And then add in a semicolon at the end of this line so that you match up with some of the good coding protocols in Python that are available to make things easier.

With all of this running through your head, it is likely that this process, and the idea of creating your own class, is going to seem really complicated. That is why we need to stop for a few minutes and look at an example of how we would want to write all of this out in Python. The code that we are going to use to help us to write out a class in the Python language will include:

```
```
class Vehicle(object):
    #constructor
    def __init__(self, steering, wheels, clutch, breaks, gears):
        self._steering = steering
        self.__wheels = wheels
        self.__clutch = clutch
        self._breaks = breaks
        self._gears = gears
    #destructor
```
```