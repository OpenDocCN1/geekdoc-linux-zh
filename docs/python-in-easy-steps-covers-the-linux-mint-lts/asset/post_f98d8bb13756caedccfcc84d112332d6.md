
Typically, instance variables contain data passed by the caller when an instance copy of the class is created. As this data is only available locally for internal use, it is effectively hidden from the rest of the program. This technique of data "encapsulation" ensures that data is securely stored within the class structure and is the first principle of Object Oriented Programming (OOP).

![](img/d06b1f1cf83677f6647237f0c7827141_177_0.png)

It is conventional to begin class names with an uppercase character, and object names with lowercase.

All properties of a class are referenced internally by the dot notation prefix `self` – so an attribute named “sound” is `self.sound`. Additionally, all method definitions in a class must have `self` as their first argument – so a method named “talk” is `talk(self)`.

When a class instance is created, a special `__init__(self)` method is automatically called. Subsequent arguments can be added in its parentheses if values are to be passed to initialize its attributes.

A complete Python class declaration could look like this example:

```python
class Critter:
    """A base class for all critter properties."""
    count = 0

    def __init__(self, chat):
        self.sound = chat
        Critter.count += 1

    def talk(self):
        return self.sound
```

It is useful to examine the class components of this example:

- The variable `count` is a class variable whose integer value gets shared among all instances of this class – this value can be referenced as `Critter.count` from inside or outside the class.
- The first method `__init__()` is the initialization method that is automatically called when an instance of the class is created.
- The `__init__()` method in this case initializes an instance variable `sound`, with a value passed from the `chat` argument, and increments the value of the `count` class variable whenever an instance of this class is created.
- The second method `talk()` is declared like a regular function, except the first argument is `self`, which is automatically incorporated – no value needs to be passed from the caller.
- The `talk()` method in this case simply returns the value encapsulated in the `sound` instance variable.

![](img/d06b1f1cf83677f6647237f0c7827141_178_0.png)

The class documentation string can be accessed via the special `__doc__` docstring attribute with `ClassName.__doc__`.

![](img/d06b1f1cf83677f6647237f0c7827141_178_1.png)

While a program class cannot perfectly emulate a real-world object, the aim is to encapsulate all relevant attributes and actions.

## Creating instance objects

An "instance" of a class object is simply a copy of the prototype created by calling that class name's constructor and specifying the required number of arguments within its parentheses. The call's arguments must match those specified by the `__init__()` method definition – other than a value for the internal `self` argument.

The class instance object returned by the constructor is assigned to a variable using the syntax `instance-name = ClassName(args)`.

Dot notation can be used to reference the methods and class variable attributes of an instance object by suffixing their name as `instance-name.method-name()` or `instance-name.attribute-name`.

Typically, a base class can be defined as a Python module file so it can be imported into other scripts where instance objects can be easily created from the "master" class prototype.

- 1. Start a new Python script by declaring a new class with a descriptive document string
    ```python
    class Bird:
        """A base class to define bird properties."""
    ```

![](img/d06b1f1cf83677f6647237f0c7827141_179_0.png)

- 2. Next, add an indented statement to declare and initialize a class variable attribute with an integer zero value
    ```python
    count = 0
    ```

- 3. Now, define the initializer class method to initialize an instance variable and to increment the class variable
    ```python
    def __init__(self, chat):
        self.sound = chat
        Bird.count += 1
    ```

- 4. Finally, add a class method to return the value of the instance variable when called – then save this class file
    ```python
    def talk(self):
        return self.sound
    ```

![](img/d06b1f1cf83677f6647237f0c7827141_180_0.png)

A constructor creates an instance of a class and is simply the class name followed by parentheses containing any required argument values.

![](img/d06b1f1cf83677f6647237f0c7827141_180_1.png)

You must not pass an argument value for the `self` argument, as this is automatically incorporated by Python.

- 5. Start another Python script by making features of the class file available, then display its document string
    ```python
    from Bird import *
    print('\nClass Instances Of:\n', Bird.__doc__)
    ```

![](img/d06b1f1cf83677f6647237f0c7827141_180_2.png)

- 6. Next, add a statement to create an instance of the class and pass a string argument value to its instance variable
    ```python
    polly = Bird('Squawk, squawk!')
    ```

- 7. Now, display this instance variable value and call the class method to display the common class variable value
    ```python
    print('\nNumber Of Birds:', polly.count)
    print('Polly Says:', polly.talk())
    ```

![](img/d06b1f1cf83677f6647237f0c7827141_181_0.png)

- 8. Create a second instance of the class, passing a different string argument value to its instance variable
    ```python
    harry = Bird('Tweet, tweet!')
    ```

- 9. Finally, display this instance variable value and call the class method to display the common class variable value
    ```python
    print('\nNumber Of Birds:', harry.count)
    print('Harry Says:', harry.talk())
    ```

![](img/d06b1f1cf83677f6647237f0c7827141_181_1.png)

- 10. Save the file in your scripts directory, then open a Command Prompt window there and run this program – to see two instances of the Bird class get created

![](img/d06b1f1cf83677f6647237f0c7827141_181_2.png)

![](img/d06b1f1cf83677f6647237f0c7827141_182_0.png)

The class variable `count` can also be referenced with `Bird.count`, but the encapsulated instance variable `sound` can only be accessed by calling an instance’s `talk()` method.

## Addressing class attributes

An attribute of a class instance can be added, modified, or removed at any time using dot notation to address the attribute. Making a statement that assigns a value to an attribute will update the value contained within an existing attribute or create a new attribute of the specified name containing the assigned value:
`instance-name.attribute-name = value`
`del instance-name.attribute-name`

Alternatively, you can use the following Python built-in functions to add, modify, or remove an instance variable:

- `getattr(instance-name, 'attribute-name')` – return the attribute value of the class instance.
- `hasattr(instance-name, 'attribute-name')` – return `True` if the attribute value exists in the instance, otherwise return `False`.
- `setattr(instance-name, 'attribute-name', value)` – update the existing attribute value or create a new attribute in the instance.
- `delattr(instance-name, 'attribute-name')` – remove the attribute from the instance.

The name of attributes automatically supplied by Python always begin with an underscore character to notionally indicate "privacy" – so these should not be modified, or removed. You can add your own attributes named in this way to indicate privacy if you wish, but in reality these can be modified like any other attribute.

- 1. Start a new Python script by making features of the Bird class available that was created here
    ```python
    from Bird import *
    ```

![](img/d06b1f1cf83677f6647237f0c7827141_183_0.png)

- 2. Next, create an instance of the class, then add a new attribute with an assigned value using dot notation
    ```python
    chick = Bird('Cheep, cheep!')
    chick.age = '1 week'
    ```

- 3. Now, display the values in both instance variable attributes
    ```python
    print('\nChick Says:', chick.talk())
    print('Chick Age:', chick.age)
    ```

![](img/d06b1f1cf83677f6647237f0c7827141_184_0.png)

The attribute name specified to these built-in functions must be enclosed within quotes.

- 4. Then, modify the new attribute using dot notation and display its new value
    ```python
    chick.age = '2 weeks'
    print('Chick Now:', chick.age)
    ```

- 5. Next, modify the new attribute once more, this time using a built-in function
    ```python
    setattr(chick, 'age', '3 weeks')
    ```

![](img/d06b1f1cf83677f6647237f0c7827141_184_1.png)

- 6. Now, display a list of all non-private instance attributes and their respective values using a built-in function
    ```python
    print('\nChick Attributes...')
    for attrib in dir(chick):
        if attrib[0] != '_':
            print(attrib, ':', getattr(chick, attrib))
    ```

- 7. Finally, remove the new attribute and confirm its removal using a built-in
