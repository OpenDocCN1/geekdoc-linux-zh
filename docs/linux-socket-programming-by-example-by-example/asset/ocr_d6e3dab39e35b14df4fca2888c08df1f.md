**NOTE**
Here you will simply learn about the domain and the protocol arguments. The discussion for the type argument will be deferred until later in the chapter.

Normally, the protocol argument is specified as zero. A zero allows the operating system to choose the correct default protocol to be used for the domain that has been selected. There are exceptions to this rule, but this is beyond the scope of the present discussion.

This leaves the domain argument to be explained. For the socketpair(2) function, this value must always be AF_LOCAL or AF_UNIX. In the last chapter, it was pointed out that the macro AF_UNIX is the equivalent of and the older macro name for AF_LOCAL. What does AF_LOCAL mean however? What does it select?

The AF_ prefix of the constant indicates the address family. The domain argument selects the address family to be used.

Chapter 4, “Socket Types and Protocols,” will expand upon the domain argument further. In that chapter you will learn about C macros with a prefix of PF_ like PF_LOCAL. For the purposes of this chapter, however, you may consider AF_ prefixed macros equivalent to the PF_ prefixed macros.

# Forming Socket Addresses

Each communication protocol specifies its own format for its networking address. Consequently, the address family is used to indicate which type of addressing is being used. The constant AF_LOCAL (AF_UNIX) specifies that the address will be formed according to local (UNIX) address rules. The constant AF_INET indicates that the address will conform to IP address rules, and so on. These are examples of address families.

Within one address family, there can be variations. You will see an example of this when you learn how to form AF_LOCAL addresses.

In the sections that follow, you will examine the format and the physical layout of various address families. This is an important section to master. Much of the difficulty that people experience with the BSD socket interface is related to address initialization.

# Examining the Generic Socket Address

Because the BSD socket interface was developed before the ANSI C standard was adopted, there was no (void *) data pointer type to accept any structure address. Consequently, the BSD solution chosen was to define a generic address structure. The generic structure is defined by the C language statement

```
#include <sys/socket.h>
```