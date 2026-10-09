The `pam_start(3)` call registers the application with the specified service. After the user is vouched for by `pam_authenticate(3)`, the application can safely trust the user's identity and privileges.

# 3.4 JAVA

Those wanting to develop Java applications that are compatible across different JVMs should follow the Java API Specification.¹ Java is not native to Linux nor UNIX, so it is out of scope of the LSB.

Applications that use the Java Native Interface (JNI)² do have native Linux object code that can and should be LSB-conformant. JNI object code can be LSB-certified.

# 3.5 `kill(3)`

Passing process ID -1 to `kill(3)` doesn't affect the calling process. This was a deliberate decision after the unpopular experiment of including the calling process in the 2.5.1 kernel.³

# 3.6 `ioctl(3)`

The LSB has its own definition of `ioctl(3)` and does not reference ISO/IEC 9945.

# reference

+   1. http://java.sun.com/reference/api/index.html
+   2. http://java.sun.com/docs/books/tutorial/native/1.1/concepts/index.html
+   3. *What does it mean to signal everybody?*, Linux Weekly News, 20 December 2001 (http://lwn.net/2001/1220/kernel.php3).