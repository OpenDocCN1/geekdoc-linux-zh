Overloading of a function is intended for closely related operations. For example, overloading a function called *square()*, once for the square of an integer and the other for the square root of a floating point number, would not be good programming practice. The variations of the overload function are not closely related. If the square() function accepted an integer and squared it, and overloaded the function to accept a floating-point number and squared it, this would be a case where operations were closely related and overloading makes sense.

# Default Function Arguments

C++ allows a parameter to have a default value if the function is called with no corresponding value. For example, if a function is called with an integer and a character in the parameter list, each of these values can be given a default value:

```
```
void price_widgets(int num_widgets = 1, char widget_type = 'A')
{
    // code for pricing widgets
    ...
}
```
```

The function is then called in the following ways:

```
```
price_widgets( 3, 'D' ); // passes values to all parameters
price_widgets( 7 ); // passes in the number of widgets,
                 // but uses the default value for the widget type
price_widgets(); // uses default values for both parameters
```
```

The first function call passes values to all the parameters. Because the second function call does not have a value for *widget_type*, the default of `A` is used. In the third function call, both parameters are not passed; the default values of 1 for the number of widgets and `A` for the widget type are used.