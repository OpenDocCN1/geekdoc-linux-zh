m is actually a pointer to a F . In fact, it points to the structure that contains the data for a particular instance from the F class.

Now that you have an object to store a F , you need to create one, just like you ask the factory to build you a new car. This is done with the following line:

```
m
```

You want to allocate memory storage space for a new fraction. The expression

```
[
```

sends a message to your newly created F class. You are asking the F class to apply the new method, but you never defined a new method, so where did it come from? The method was inherited from a parent class.

You are now ready to set the value of your F . The program lines

```
[
```

do just that. The first message statement sends the $ message to m . The argument that is supplied is the value 1. Control is then sent to the $ method you defined for your F class. The Objective-C runtime system knows that it is the method from this class to use because it knows that m is an object from the F class.

Inside the $ method, the single program line in that method takes the value passed in as the argument and stores it in the instance variable n . So, you have effectively set the numerator of m to 1.

The message that invokes the $ method on m follows next, and works in a similar way.

With the fraction being set, Program 18.2 then calls the two getter methods n and d to retrieve the values of the corresponding instance variables from m . The results are then passed to p to be displayed.

The program next invokes the p method. This method displays the value of the fraction that is the receiver of the message. Even though you saw in the program how the numerator and denominator could be retrieved using the getter methods, a separate p method was also added to the definition of the F class for illustrative purposes.

The last message in the program

```
[
```

frees the memory that was used by your F object.

# Defining a C++ Class to Work with Fractions

Program 18.3 shows how a program to implement a F class might be written using the C++ language. C++ was invented by Bjarne Stroustrup at Bell Laboratories, and was the first object-oriented programming language based on C—at least to my knowledge! Note when compiling this program—if you are using an integrated development environment (IDE) that can compile C and C++ programs, and you have been writing C programs to this point, your IDE might try to save the program as a .c file. That would then generate a series of error messages that can be avoided by saving the file with a .cpp extension, ensuring that your IDE compiles the program as a C++ program.