# Chapter 8 · The java.lang and java.Util Packages

If you want to call sitOnGold() on each dragon in the set, you can now do it like this:

```
for (Dragon d:dragons)
  d.sitOnGold();
```

The code above is ideal to the following pre-Java 1.5 code:

```
Iterator iter = dragons.iterator();
while (iter.hasNext()) {
  Dragon d = dragons.next();
  d.sitOnGold();
}
```

The Java 5.0 version is perfectly understandable (once you get used to the colon notation), it is shorter by 60 percent and eliminates the Iterator and the cast. The new syntax is

```
for (type variable_name : collection)
```

The type and variable name form a declaration whose through the loop, the variable takes on a different block following the statement. Each pass contains the values of the collection, presented in the order that an Iterator would value; the values are (This is expected, since an Iterator is created and used as the underlying mechanism, even though it can't be seen.)

The Collection appears after the colon can be anything that implements the Collection interface: a List (of Vectors are the most common example), a Set, or the keys or values of a Map.

The enhanced for loop, like generic collections, provides a way to write code that is cleaner, less vulnerable to errors, and easier to read.

# Scanning and Formatting Text

Java contains extensive facilities for dealing with text. The relevant classes reside in the java.lang and java.util packages. Text can present special problems for programs and programmers. Text contains meaning, which is expressed in language, and both meaning and language are very deep concepts, implicitly involved in what makes us human. No wonder computers have trouble with text!

The problems fall into two areas: how to extract meaning from existing text and how to create grammat correct text that contains meaning. One way to address these problems is to get a Ph.D. in computational linguistics and dedicate your life to figuring it all out. But if your goal is just to pass the Programmer's Exam, all you need to do is learn about Java's facilities for scanning and formatting text.