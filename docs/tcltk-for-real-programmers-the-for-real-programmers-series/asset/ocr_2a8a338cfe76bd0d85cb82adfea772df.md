# 7.1 Namespaces and Scoping Rules

There are a few points to note in this example:

+   - The procedure getUnique can be declared as an exported name before the procedure is defined.
- After the uniqueNumber namespace is defined, there are two namespaces visible from the global scope—the ::uniqueNumber namespace and the ::tcl interpreter. The ::tcl namespace is always present when the Tcl interpreter is running.
- The namespace import ::uniqueNumber:* imports all exported entities from ::uniqueNumber into the global scope.
- The value of the staticVar variable can be accessed via the namespace eval. ::uniqueNumber::staticVar.
- The staticVar variable is initialized by the line variable staticVar 0 when the namespace is created. This code is equivalent to set staticVar 0 arguments to namespace eval, which would cause the variable to be defined at the top scope of the uniqueNumber namespace.

# 7.1.7 Namespace Nesting

If procedures in two namespaces need functionality that exists in a third namespace, there are a couple of options. They can create a shared copy of the third namespace in the scope of the first two namespaces, or each can create a copy of the third namespace nested within its own namespace scope.

One advantage of nesting the third namespace is that it creates a unique copy of the persistent data defined within the third namespace. If a namespace is shared, then that data is shared.

The next example shows the uniqueNumber namespace being nested within two separate namespaces (Package1 and Package2). This allows each procedure in Package1 and Package2 to get unique numbers with no gaps between numbers.

If the uniqueNumber namespace were created at the global level and shared by Package1 and Package2, then whenever either package called getUnique the unique number would be incremented.