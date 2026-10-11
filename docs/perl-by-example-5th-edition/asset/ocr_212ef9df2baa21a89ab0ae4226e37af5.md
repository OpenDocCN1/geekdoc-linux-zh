```
EXAMPLE 12.11 (CONTINUED)

(Output)
2 Science
4 piano flute harp

4 $VAR1 = {
    'Teacher' => [
        'Subjects' => [
            'Science',
            'Math',
            'English'
        ]
    ],
    'Musician' => {
        'Instruments' => [
            'piano',
            'flute',
            'harp'
        ]
    }
};
```

+   EXPLANATION
+   1 The reference *Shashref* is assigned an anonymous hash consisting of two keys, *Teacher* and *Musician*. Notice that the entire hash structure is enclosed in curly braces rather than parentheses. That means *Shashref* is getting the address of this set of key/value pairs. The rest of this example is just like Example 12.10.
+   2 To dereference *Shashref*, the arrow operator is used to get to the first key, *Teacher* or *Musician*, and then arrows will be used to separate the remaining nested keys/value pairs. The final arrow refers to the first element of the array of values associated with *Subjects*, which is *Science*.
+   3 To get all the values from the anonymous array associated with the key, the @ symbol precedes a block consisting of the reference and its nested keys, each key separated with the arrow operator.
+   4 The *Dumper* function requires a reference, *Shashref*.

# 12.1.5 References and Subroutines

**Anonymous Subroutines.** A reference to an anonymous subroutine is created by using the keyword *sub* without a subroutine name. The expression is terminated with a semicolon. For more on using anonymous subroutines, see Section 14.3.1, “What Is a Closure?”