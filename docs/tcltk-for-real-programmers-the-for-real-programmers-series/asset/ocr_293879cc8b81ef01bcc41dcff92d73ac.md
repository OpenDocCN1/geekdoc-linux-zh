# 7.1 Namespaces and Scoping Rules

+   * Variables created in a namespace scope (outside a local procedure scope) can be accessed by any procedure that is being evaluated within that namespace.
* While a procedure defined within a namespace is being evaluated, creates a local scope within that namespace, not within the global namespace.

Namespaces are similar to local procedure scopes in that:

+   * Code being evaluated within a namespace can access variables and procedures defined in the global space.
* All namespaces are contained within the global scope.
* Namespaces can nest within each other.

Namespaces also have some unique features:

+   * A namespace can declare certain items (procedures or variables) to be exportable. Exportable items can be made visible in the global scope.
* A nested namespace can keep procedures and variables hidden from higher level namespaces.

The following diagram shows the scopes in a script that contains two namespaces (example and demo), each of which contains procedures named proc1 and proc2. Because the procedures are in separate namespaces, they are different procedures. If a script tried to define two proc1 procedures at the global level, the second definition would overwrite the first.

In this example, example::proc1 and example::proc2 are procedures that are both called independently, while demo::proc2 is called from demo::proc1. The demo::proc2 is displayed within demo::proc1 to show that the procedure local scopes nest within a namespace just as nested within the stack example in the previous chapter.