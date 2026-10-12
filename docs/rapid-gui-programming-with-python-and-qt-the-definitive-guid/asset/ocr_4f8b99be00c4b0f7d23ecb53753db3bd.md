from object, so our class is new-style. Then we create some static data. First we create a dictionary that maps names to conversion factors. We can't use "in" as an argument name because it is a Python keyword, so we insert it into the dictionary separately using the [] operator. We also create a set of the characters that are valid in floating-point numbers.

```
```
def __init__(self, length=None):
    if length is None:
        self.__amount = 0.0
    else:
        digits = ""
        for i, char in enumerate(length):
            if char in Length.numbers:
                digits += char
            else:
                self.__amount = float(digits)
                unit = length[i:].strip().lower()
                raise ValueError, "need an amount and a unit"
                self.__amount /= Length.convert[unit]
```
```

Inside the initializer, the local variables length, digits, i, char, and unit all go out of scope at the end of the method. We refer only to one instance variable, self.__amount. This variable always holds the given length in meters, no matter what units were used in the initializer, and is accessible from any method. We also refer to two static variables, Length.numbers and Length.convert.

When a Length object is created, Python will call the `__init__()` method. We give the user two options: Pass no arguments, in which case the length will be 0 meters, or pass a string that specifies an amount and a unit with optional whitespace separating the two.

If a string is given, we want to iterate over the characters that are valid in numbers, and then take the remainder to be the units. Python's `enumerate()` function returns an iterator that returns a tuple of two values on each iteration, an index number starting from 0, and the corresponding item from the sequence. So if the string in length was "7 mi", the tuples returned would be (0, "7"), (1, " "), (2, "m"), and (3, "i"). We can unpack a tuple in a for loop simply by providing enough variables.

As long as we retrieve characters that are in the numbers set we add them to our digits string. Once we reach a character not in the set, we attempt to convert the digits string to a float, and take the rest of the length string to be the units. We strip off any leading and trailing whitespace from the units string, and lowercase the string. Finally, we calculate how many meters the given length is by using the conversion factor from the static convert dictionary.