# 44

# appcert

# Environment Variables

AB2_DEFAULTSERVER

Fully qualified URL that identifies the default AnswerBook2 server to use. For example: http://imaserver.eng.sun.com:8888/

# Attributes

See attributes(5) for descriptions of the following attributes:

| Attribute Type | Attribute Value |
| Availability | SUNWab2m |

# See Also

ab2cd(1M), ab2admin(1M), attributes(5)

# appcert — Examine Application-Level Products for Unstable Use of Solaris Interfaces

# Synopsis

```
/bin/appcert [-h] [-n] [-f infile] [-w working_dir] [-B] [-L] [-S] obj|dir...
```

# Description

Use the appcert command, new in the Solaris 9 Operating Environment, to examine an application's conformance to the Solaris Application Binary Interface (ABI). The Solaris defines the runtime library interfaces in Solaris that are safe and stable for application use. More specifically, appcert identifies all dependencies on unstable runtime interfaces. It can also identify other risks that might break the product in subsequent release of Solaris.

appcert checks for the following elements:

+   - Private symbol usage in Solaris libraries. These private symbols, are functions or data, are not intended for developer consumption. Solaris libraries use these interfaces to call one another. These symbols might change their behavior or ever disappear altogether (so-called demod symbols), so it is a good practice to make sure your application does not depend on any of them.
- Static linking references, specifically, to static linking of archives libc.a, libsocket.a, and libnsl.a instead of dynamically linking private symbol calls from one files of the shared object. Because the semantics change one release to another, it is not a good practice to “hardwire” library code into your binary objects.