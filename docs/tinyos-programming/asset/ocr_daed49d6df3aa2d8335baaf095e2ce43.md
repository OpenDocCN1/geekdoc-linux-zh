its subcomponents at run-time, storing pointers and resolving operations through another level of call indirection. In contrast, as a nesC Facade is defined through naming (pass through wiring) at compile-time, there is no run-time cost.

# Applicable when

+   - An abstraction, or series of related abstractions, is implemented across several separate components.
+   - It is preferable to present the abstraction in whole rather than in parts.

# Structure

![](bbox=[0.3, 0.38, 0.85, 0.6])

# Participants

+   - Facade: the uniform presentation of a set of related services.
+   - SvcImpl: the separate implementations of each service composing the Facade.

# Sample 1.x code

The Matchbox filing system uses a Facade to present a uniform filesystem abstraction. File operations are all implemented in different components, but the top-level Matchbox configuration provides them in a single place. Each of these components depends on a wide range of underlying abstractions, such as a block interface to non-volatile storage; Matchbox wires them appropriately, resolving all of the dependencies.

```
configuration Matchbox {
    provides {
        interface FileRead[uint8_t fd];
        interface FileWrite[uint8_t fd];
        interface FileDir;
        interface FileRename;
        interface FileDelete;
    }
}

implementation {
    // File operation implementations
    components Read, Write, Dir, Rename, Delete;

    FileRead = Read.FileRead;
    FileWrite = Write.FileWrite;
```