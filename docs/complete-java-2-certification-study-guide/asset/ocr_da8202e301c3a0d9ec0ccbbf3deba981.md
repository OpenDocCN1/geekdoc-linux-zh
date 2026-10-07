# Chapter 4 • Converting and Casting

Assuming that a desired cast survives compilation, a second check must occur at runtime. The second check determines whether the class of the object being cast is compatible with the new type. (This could not be made at compile time, because the object being cast did not exist then.) Here, compatible means that the class can be converted according to the conversion rules discussed in the previous sections. The following rules cover the most common runtime cases:

+   - If Newtype is a class, the class of the expression being converted must be Newtype or must inherit from Newtype.
- If Newtype is an interface, the class of the expression being converted must implement Newtype.

It is definitely time for some examples! Look once again at the Fruit/Citrus hierarchy you saw earlier in this chapter, which is repeated in Figure 4.10.
Consider the following code:

```
1. Grapefruit g, gl;
2. Citrus c;
3. Tangelo t;
4. g = new Grapefruit(); // Class is Grapefruit
5. c = g; // Legal assignment conversion,
   // no cast needed
6. g = (Grapefruit)c; // Legal cast
7. t = (Tangelo)c; // Illegal cast
   // throws an exception
```

# FIGURE 4.10 Fruit hierarchy (reprise)

![](bbox=[0.258, 0.597, 0.575, 0.903])