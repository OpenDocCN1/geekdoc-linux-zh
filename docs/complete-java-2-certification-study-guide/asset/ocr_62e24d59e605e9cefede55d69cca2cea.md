# The Wrapper Classes 267

which boxes a double into a Double. The following change, which boxes an int into an Integer, also works:

Integer wi = 123;

> Boxing also occurs when a method's return type is a wrapper. You do not need to explicitly construct a wrapped object. For example, you can now get away with the following:

```
Double area(double radius) {
  return Math.PI * radius * radius;
}
```

The Java 5.0 compiler also allows you to unbox a wrapped value. Unboxing is the automatic extraction of a wrapped value. Unboxing happens when a wrapper object appears as an boolean or numerical operation, as shown in the example below:

+   1. Integer wi = 234;
2. int times9 = wi * 9;

Line 1 boxes to construct a wrapper object. Line 2 multiplies the wrapper by a (primitive) int. Prior to 5.0, it would not have compiled, so the 5.0 compiler edits that extracts (unboxes) the primitive value wrapped in wi and multiplies by 9. We can now rewrite the area() method as follows:

```
Double area(double radius) {
  return Math.PI * radius * radius;
}
```

This version of the method shows the power and convenience of boxing and unboxing. However, you should be aware that the boxing and unboxing syntaxes are just abbreviations. They do not eliminate the creation of wrapper objects or the extraction of wrapped values; they just hide these operations from the untrained eye. Consider the following code:

```
Double rad=0;
for (rad<=1; rad+=1.0e-9)
System.out.println(rad);
```

This code calls area() one billion times. The loop's increment step constructs (via the boxing mechanism) one billion wrapper objects, which later are garbage collected; it also extracts one billion wrapped values (via the unboxing mechanism). The radius() method unboxes and boxes once during each of its billion calls. The innocent-looking method has phenomenally more overhead than equivalent code that uses primitive primitives, but the overhead is visible only to people who understand the underlying mechanisms.