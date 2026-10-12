![](bbox=[0.11, 0.09, 0.21, 0.19])

5 Next, create an instance of each derived class
rect = Rectangle()
trey = Triangle()

6 Now, call the class method inherited from the base class, passing arguments to assign to the class variables
rect.set_values(4, 5)
trey.set_values(4, 5)

7 Finally, display the result of manipulating the class variables inherited from the base class
print('Rectangle Area:', rect.area())
print('Triangle Area:', trey.area())

8 Save the file in your scripts directory, then open a Command Prompt window there and run this program – to see output get displayed using inherited features

```
```
Command Prompt

C:\MyScripts>python inher it.py
Rectangle Area: 20
Triangle Area: 10.0

C:\MyScripts>■
```
```

![](bbox=[0.11, 0.73, 0.22, 0.84])

A class declaration can derive from more than one class by listing multiple base classes in the parentheses after its name in the declaration.