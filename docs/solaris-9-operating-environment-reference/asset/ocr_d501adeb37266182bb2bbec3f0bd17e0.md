# psig, pstack, pstop, ptime, ptree — Proc Tools

Synopsis

```
/usr/proc/bin/psig pid...
/usr/proc/bin/pstack pid...
/usr/proc/bin/pstop pid...
/usr/proc/bin/ptree [[pid|user]...]
/usr/proc/bin/ptime command [arg...]
```

Description

See proc(1).

# pushd — Change Working Directory

Synopsis

```
csh
pushd [+n | dir]
```

Description

See cd(1).

# pvs — Display the Internal Information of Dynamic Objects

Synopsis

```
/usr/bin/pvs [-Cdlnorsv] [-N name] file...
```

Description

Use the pvs command to display any internal version information contained in an executable and linking format (ELF) object file. Commonly, ELF files are dynamic executables, shared objects, and possibly relocatable objects. This version information falls into one of two categories.

+   * Version definitions describe the interfaces made by an ELF file. Each version definition is associated with a set of global symbols provided by the file. Version definitions can be assigned to a file during its creation by the link editor, using the -M option and the associated mapfile directives (see the Linker and Libraries Guide for more details).

+   * Version dependencies describe the binding requirements of dynamic objects on the versions of any shared object dependencies. When a dynamic object is built with a shared object, the link-editor records information within the dynamic