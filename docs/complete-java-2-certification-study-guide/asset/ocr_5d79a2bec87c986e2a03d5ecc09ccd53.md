# FIGURE 1.3 An irregular multi-dimension array

![](bbox=[0.198, 0.149, 0.555, 0.396])

Figure 1.3 shows an array whose elements are an array of 3 ints, an array of 4 ints, and an array of 2 ints. Such an array may be created like this:

```
int[] myInts = { {1, 2, 3}, {91, 92, 93, 94}, {2001, 2002} };
```

When you realize the outermost array is a single-dimension array containing references, you understand that you can replace any of the references with a reference to a different subordinate array, provided the new subordinate array is of the right type. For example, you can do the following:

```
int[] myInts = { {1, 2, 3}, {91, 92, 93, 94}, {2001, 2002} };nint[] replacement = {1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12};
myInts[1] = replacement;
```

# Importing

The term “import” can be confusing. In common speech, import means to bring something from abroad into one's territory. In the Java context, it's natural to wonder what is getting brought in, and where it is getting into. A common mistake is to guess that importing has something to do with class loading. It's a reasonable mistake, since the class loader is the only obvious entity that brings something (class definitions) into somewhere (the Java Virtual Machine). However, the guess is wrong.

What gets brought in is the import class's name. The name is brought into the source file's namespace. A namespace is a kind of place—not a physical place, but an abstract place such as