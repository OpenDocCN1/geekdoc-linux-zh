# TABLE 3.1 Access and Static Imports

| Feature Access Mode | Feature May Be Statically Imported into Same-Package Source File | Feature May Be Statically Imported into Different-Package Source File |
| - | - | - |
| Public | Yes | Yes |
| Protected | Yes | No |
| Default | Yes | No |
| Private | No | No |

# native

The native modifier can only refer to methods. Like the abstract modifier, native indicates that the body of a method is to be found elsewhere. In the case of abstract methods, the body is in a subclass; with native methods, the body lies entirely outside the Java Virtual Machine (JVM), in a library.

Native code is written in a non-Java language, typically C or C++, and compiled for a target machine type. (Thus Java's platform independence is violated.) People who port Java to new platforms implement extensive native code to support GUI components, network communication, and a broad range of other platform-specific functionality. However, it is rare for application and app programmers to write native code.

One technique, however, is of interest in light of the last section's discussion of static code. When a native method is invoked, the library that contains the native code must be loaded and available to the JVM; if it is not loaded, there will be a delay. The library is loaded by calling System.loadLibrary("library_name"), and to avoid a delay, it is desirable to make this call as early as possible. Often programmers use the technique shown in the following code sample, which assumes the library name is MyNativeLib:

+   1. class NativeExample {
2. native void doSomethingLocal(int i);
3.
4. static {
5. System.loadLibrary("MyNativeLib");
6. }
7. }

Notice the native declaration on line 2, which declares that the code implements doSomethingLocal(i) resides in a local library. Lines 4–6 are static initializer code, so they are executed at the time that class NativeExample is loaded; this ensures that the library is available by the time somebody needs it.