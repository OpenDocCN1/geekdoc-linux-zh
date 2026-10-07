Figure 3.2 shows the legal access types by subclasses. A method with some particular access type may be overridden by a method with a different access type, provided there is a path in the figure from the original type to the new type.

# FIGURE 3.2 Legal overridden method access

![](bbox=[0.211, 0.219, 0.617, 0.263])

+   The rules for overriding can be summarized as:
- A private method may be overridden by a private, default, protected, or public method.
- A default method may be overridden by a default, protected, or public method.
- A protected method may be overridden by a protected or public method.

Figure 3.3 shows the illegal access types for subclasses. A method with some particular access type may not be shadowed by a method with a different access type, if there is a path in the figure from the original type to the new type.

# FIGURE 3.3 Illegal overridden method access

![](bbox=[0.193, 0.512, 0.617, 0.556])

+   The illegal overriding combinations can be summarized as follows:
- A default method may not be overridden by a private method.
- A protected method may not be overridden by a default or private method.
- A public method may not be overridden by a protected, default, or private method.

# Other Modifiers

In this section, we will discuss Java’s other modifiers, namely:

+   - final
- abstract
- static
- native
- transient
- volatile
- synchronized