# Obsolete Library

An obsolete library is one whose use is deprecated and that might, in some future release, be removed from Solaris. appcert flags these because applications depending on them might not run in future releases of Solaris. All interfaces, including Private ones, in an obsolete library are frozen and will not change.

# Use of sys_errlist or sys_nerr

Direct use of the symbols sys_errlist or sys_nerr presents a risk in which reference might be passed past the use of the sys_errlist array. These symbols are deprecated in 32-bit versions of Solaris and are absent altogether in 64-bit versions. Use strerror(3C)

# Use of Strong vs. Weak Symbols

The "strong" symbols (for example, socket) associated with "weak" symbols (for example, socket) are reserved as private (their behavior could change in the future). Your application should directly reference only the weak symbol (usually the strong symbols begin with _).

> Note — Under certain build environments, the strong/private symbol dependency recorded into your binary instead of the weak/public one, even though the source code does not appear to reference the private symbol. Nevertheless, you should take steps to trace down why this problem is occurring and fix the dependency.

# Bugs

The terms "public" and "private" as equivalent to "stable" and "unstable" are unfortunately somewhat confusing. In particular, experimental or evolving interfaces are Public in the sense that they are documented and their use is encouraged. But, they are unstable because an application built with them might not run on subsequent releases. Thus, they are classified as Private for appcert's purposes until they are no longer evolving. Convolving, obsolete interfaces eventually disappear, and so are unstable, even though they have been Public and stable in the past and are still treated as Public by appcert. Fortunately, these two situations are rare.

# Attributes

See attributes(5) for descriptions of the following attributes.

| Attribute Type | Attribute Value |
|---|---|
| Availability Interface Stability | SUNmapct Stable |

# See Also

```
cc(1), find(1), isalist(1), 1d(1), ldd(1), 1d.so(1), pvs(1), dlopen(3DL), strerror(3C), intro(4), attributes(5)
```

Linker and Libraries Guide