Keymaps only support mapping between integers. If you need, e.g. to map from strings to a Local Keyspace, you will need to build your own map.

# Related patterns

+   - Keyspace: A Keymap establishes a map from one keyspace to another.

# 10.5 Structural: Placeholder

# Intent

Easily change which implementation of a service an entire application uses. Prevent inadvertent inclusion of multiple, incompatible implementations.

# Motivation

Many TinyOS systems and abstractions have several implementations. For example, there are many ad hoc tree routing protocols, including two (Ctp, Lqi) in the TinyOS core, but they all expose the same interfaces (StdControl, Send, Receive, etc.). The standardized interface allows applications to use any of the implementations without code changes. Simpler abstractions can also have multiple implementations. For example, the LedsC component actually turns the LEDs on and off, while the NoLedsC component, which provides the same interface, has null operations. During testing, LedsC is useful for debugging, but in deployment it is a significant energy cost and usually replaced with NoLedsC.

Sometimes, the decision of which implementation to use needs to be uniform across an application. For example, if a hypothetical network health monitoring subsystem wires to Ctp, while an application uses Lqi, two routing trees will be built, wasting resources. As every configuration that wires to a service names it, changing the choice of implementation in a large application could require changing many files. Some of these files, such as the network health monitor might be part of the system; an application writer should not have to modify them.

One option is for every implementation to use the same component name, and put them in separate directories. Manipulating the nesC search order allows an application to select which version to use. However, this forces every implementation of the placeholder into a separate directory and precludes the possibility of including two implementations, even if they can interoperate.