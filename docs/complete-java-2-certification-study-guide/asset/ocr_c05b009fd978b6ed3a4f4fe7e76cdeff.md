# Object Reference Casting

Although an object's class is unchanging, it may be referenced by variables of different types. For example, consider a stack. It is constructed by calling new Stack(), so its class really is Stack. Yet at various moments during the lifetime of this object, it may be referenced by variables of type Stack (of course), or of type Vector (Stack inherits from Vector), or of type Object (because everything inherits from Object). It may even be referenced by variables of type Serializable, which is an interface, because the Stack class implements the Serializable interface. This situation is shown in Figure 4.9.

# FIGURE 4.9 Many variable types, one class

![](bbox=[0.198, 0.287, 0.781, 0.555])

Few rules govern object casting because a large number of obscure cases must be covered. For the exam, the important rules to remember when casting from Old1type to Newtype are as follows:

+   - When both Old1type and Newtype are classes, one class must be a subclass of the other.
- When both Old1type and Newtype are arrays, both arrays must contain reference types (not primitives), and it must be legal to cast an element of Old1type to an element of Newtype.
- You can always cast between an interface and a nonfinal object.