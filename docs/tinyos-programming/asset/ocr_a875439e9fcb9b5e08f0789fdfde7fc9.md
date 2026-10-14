component. This attribute is needed for when C code needs to call nesC code (e.g. in TOSSIM).

+   - @hwevent: this function will be called as a result of a hardware interrupt. Implies spontaneous.
+   - @atomic_hwevent: this function will be called as a result of a hardware interrupt, and will execute in an atomic section. Implies spontaneous. The distinction between this attribute and @hwevent is needed so nesC can know whether additional atomic sections are needed.
+   - @atmostonce: this interface must be wired to zero or one times.
+   - @atleastonce: this interface must be wired one or more times.
+   - @exactlyonce: this interface must be wired to once, no more, no less.
+   - @integer: this type parameter to a generic component must be an integer. This attribute allows generic components to use integer operations (arithmetic, shifts, bit-operations) on the type, which is important for things like scaling timers.
+   - @number: this type parameter to a generic component must be an integer or floating-point type. This attribute allows generic components to use arithmetic operations on the type.
+   - @combine: this attribute is used to specify a combine function for a type when the type is declared. It takes a parameter, a string of the name of the combine function.

Earlier versions of nesC used gcc's attribute syntax to specify these attributes, however this is now deprecated. You may however still see it in some older code, e.g. in TinyOS 1.x:

```
module RealMain { ... }
implementation {
  int main() __attribute__ ((C, spontaneous)) {
  ...
```

# 8.5 Exercises

+   1. The standard QueueC implementation uses an array to store the queue. Write an alternative implementation that uses a linked list. The maximum size of the list should be a parameter to the generic component's constructor.
+   2. Extend your linked-list to provide an additional interface, List, which allows insertion, deletion, and peeking at any point in the list.
+   3. Write a stack data structure component that takes a max stack depth and data type as parameters.
+   4. Write an additional dispatch layer on top of AM, which provides a parameterized interface to a single AM id by adding a one-byte header.