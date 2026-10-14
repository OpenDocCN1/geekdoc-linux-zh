```
components LedsC as Leds;
CsmaP.Leds -> Leds;
}
```

Listing 10.5 The CC2420CsmaC uses a Facade

# Known uses

Stable, commonly used abstract boundaries such as radio stacks (CC2420CsmaC, CC1000CsmaRadioC) and storage (BlockStorageC) often use a Facade. This allows them to implement complex abstractions in smaller, distinct parts, which simplifies code.

# Consequences

The key aspects of the Facade pattern are:

+   - Provides an abstraction boundary as a set of interfaces. A user can easily see the set of operations the abstraction support, and only needs to include a single component to use the whole service.
+   - Presents the interfaces separately. A user can wire to only the needed parts of the abstraction, but be certain everything underneath is composed correctly.

A Facade is not always without cost. Because the Facade names all of its subparts, they will all be included in the application. While the nesC compiler attempts to remove unreachable code, this analysis is necessarily conservative and may end up keeping much useless code. In particular, unused interrupt handlers are never removed, so all the code reachable from them will be included every time the Facade is used. If you expect applications to only use a very narrow part of an abstraction, then a Facade can be wasteful.

# Related patterns

+   - Placeholder: a placeholder allows easy selection of the implementation of a group of interfaces, while a Facade allows easy use of a group of interfaces. An application may well connect a placeholder to a Facade.

# 10.7 Behavioral: Decorator

# Intent

Enhance or modify a component's capabilities without modifying its implementation. Be able to apply these changes to any component that provides the interface.

# Motivation

We often need to add extra functionality to an existing component, or to modify the way it works without changing its interfaces. For instance, the standard LogStorageC component provides a LogWrite interface to log data to a region of flash memory. In some circumstances, we would like to introduce a RAM write buffer on top of the interface. This would reduce the number of times the application talks to the flash chip, improving performance and conserving energy.