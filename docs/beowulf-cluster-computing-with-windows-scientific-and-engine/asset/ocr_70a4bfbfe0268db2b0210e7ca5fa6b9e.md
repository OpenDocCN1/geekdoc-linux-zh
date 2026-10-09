![](bbox=[0.0, 0.15, 0.75, 0.48])

Named pipe and mailslot implementation.

pipe or mailslot is located is eventually invoked. There are several reasons why FSDs in kernel mode implement named pipes and mailslots, the main one being that they integrate with the object manager namespace and can use file objects to represent opened named pipes and mailslots. This integration results in several benefits:

+   The FSDs use kernel-mode security functions to implement standard Windows 2000 security for named pipes and mailslots.

+   Applications can use CreateFile to open a named pipe or mailslot because FSDs integrate with the object manager namespace.

+   Applications can use Win32 functions such as ReadFile and WriteFile to interact with named pipes and mailslots.

+   The FSDs rely on the object manager to track handle and reference counts for file objects representing named pipes and mailslots.

+   The FSDs can implement their own named pipe and mailslot namespaces, complete with subdirectories.