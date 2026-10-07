# Chapter 8 · The java.lang and java.Util Packages

In addition to Lists and Sets, Maps may also be generic. To make a Map generic, you specify a type for the keys and a second type for the values, as shown in the following example:

```
TreeMap<String, Dragon> nameToDragon;
nameToDragon = new TreeMap<String, Dragon>();
```

The code above creates a Map whose keys are strings and whose values are dragons. Note that the angle-brackets and constructor now contain two type names, separated by comma. The first type is the key type; the second is the value type. The Iterators of the Map's keys and values are generic:

```
Iterator<String> iterator = nameToDragon.keySet();
Iterator<Dragon> dragonIterator = nameToDragon.values().iterator();
```

Generic Lists, Maps, and Iterators provide a powerful compile-time check on your code, by guaranteeing that the right type of object can be stored. They save your typing some effort by eliminating many casting operations. Your code can become even more concise with the use of enhanced loops, which are discussed in two sections. Before introducing enhanced loops, let's see how generic classes are described in the API pages.

# Generics and the API Pages

Learning to use generic collections involves getting used to the angle-bracket notation. Angle brackets show up in the API pages for Java's generic classes and interfaces. In order to understand the APIs, you need to be able to read them!

Let's start with the page for the java.util Set interface. (If there's a computer nearby, you might want to look at the page at this point.) Up to Java Release 1.4, the page header said

# Interface Set

Now it says

```
Interface Set<E>
```

The E in the angle brackets tell you that this interface is generic. That is, you can think of it as a Set of something. Of whatever you would like, we'll call it E. Throughout the API page, E will stand for whatever type a programmer specifies in the declaration of the Set. E will show you in the method summaries in a variety of ways.

Up to Java Release 1.4, the method summary for add() was

```
boolean add(Object o)
```

Now it's

```
boolean add(E o)
```