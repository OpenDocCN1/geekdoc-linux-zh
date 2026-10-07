# How to Create a Reference to a Primitive

This is a useful technique if you need to create the effect of passing primitive values by reference. Simply pass an array of one primitive element over the method call, and the called method can now change the value by the caller. To do so, use code like this:

```
public class PrimitiveReference {
    public static void main(String[] args) {
        int [] myArray = { 1 };
        modifyIt(myValue);
        System.out.println("myValue contains " + myArray[0]);
    }
    public static void modifyIt(int [] value) {
        value[0]++;
    }
}
```

> In some JVMs, the reference value is actually the address of an address. This second address refers to the real data. This approach, called double indirection, allows the garbage collector to reclaim objects to reduce memory fragmentation.

When Java code appears to store objects in variables or pass objects to method calls, the object references are stored or passed. Consider this code fragment:

+   1. Button btn;
2. btn = new Button("Pink");
3. replacer(btn);
4. System.out.println(btn.getLabel());
5.
6. public void replacer(Button replaceMe) {
7. replaceMe = new Button("Blue");
8. }

Line 2 constructs a button and stores a reference to that button in btn. In line 3, a copy of the reference is passed into the replacer( ) method. Before execution of line 7, the value in replaceMe is a reference to the Pink button. Then line 7 constructs a second button and stores a reference to the second button in replaceMe, thus overwriting the reference to the Pink button.