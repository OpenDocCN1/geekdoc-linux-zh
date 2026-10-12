we might have used type testing, even though this is often poor practice in object-oriented programming.

```
    def __repr__ (self) :
        return "Length('\%.6fm'" % self.__amount
```

```
    def _str_ (self) :
        return "%.3fm" % self._amount
```

Python's floating-point accuracy depends on the compiler it was built with, but it is very likely to be accurate to much more than the six decimal places we have chosen to use for our "representation" method.

For the string representation, we don't need to be as accurate, nor do we need to return a string that can be eval()\d, so we just return the raw length and the meters unit. If users of our Length class want a string representation with a different unit, they can use to( \u2014for example, "$5 miles" % length.Length("200 ft").to("miles").

```
    def _add (self, other) :
        return Length("%fm" % (self._amount + other._amount))
```

```
    def _iadd (self, other) :
        self._amount += other._amount
        return self
```

We have used two special methods to support addition. The first supports binary+ with a length operand on either side. It constructs and returns a new Length object. The second supports += for incrementing a length by another length. They allow us to write code like this:

```
x = length.Length("30ft")
y = length.Length("250cm")
z = x + y     # z == Length('11.643554m')
x += y        # x == Length('11.643554m')
```

It is also possible to implement _radd_ ( 1 ) for mixed-type arithmetic, but we have not done so because it does not make sense for the Length class.

We will omit the code that provides support for subtraction since it is almost identical to the code for addition (and is in the source file).

```
    def _mul_ (self, other) :
        if isinstance (other, Length) :
            raise ValueError, \ \n    "Length * Length produces an area not a Length"
        return Length("%fm" % (self._amount * other))
```