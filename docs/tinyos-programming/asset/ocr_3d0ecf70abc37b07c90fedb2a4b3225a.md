is really shorthand for

```
uses interface Leds as Leds;
```

Generally, the keyword as is a useful tool for making components and their requirements clearer, similarly to how variable and function names greatly affect code readability.

# Programming Hint 1 USE THE "AS" KEYWORD LIBERALLY.

# 3.1.3 Clustering interfaces

The LedsP example shows one further detail about signatures: they can cluster used and provided interfaces together. For example, these two versions of PowerupC are equivalent:

```
configuration PowerupC {
  uses interface Boot;
  uses interface Leds;
}
```

```
configuration PowerupC {
  uses {
    interface Boot;
    interface Leds;
  }
}
```

Listing 3.5 PowerupC and an alternative signature

As these two are equivalent, there is no syntactical or code efficiency advantage to either approach: it is a matter of style and what is more legible to the reader. Often component signatures declare the interfaces they provide first, followed by the interfaces they use. This lets a reader clearly see the available functionality and dependencies. For very complex components that perform many functions, however, this approach breaks down, and signatures place related interfaces close to one another.

TinyOS detail: The names of all of the components described above end in the letters C and P. This is not a requirement. It is a coding convention used in TinyOS code. Components whose names end in C are abstractions that other components can use freely: the C stands for "component." Some component names end in P, which stands for "private." In TinyOS, P components should not be used directly, as they are generally an internal part of a complex system. Components use these two letters in order to clearly distinguish them from interfaces.

# 3.2 Interfaces

Interfaces describe a functional relationship between two or more different components. The role a component plays in this relationship depends on whether it provides or uses the interface. Like components, interfaces have a one-to-one mapping between names and files: the file Leds.nc contains the interface Leds while the file Boot.nc contains