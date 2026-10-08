# ldd

# 657

# Options

ldd can also check the compatibility of filename with the shared objects it uses. With each of the following options, ldd prints warnings for any unresolved symbol references that would occur if filename were executed.

+   -c Disable any configuration file in use. Configuration files can be used to alter default search paths, provide a directory cache, and provide alternative object dependencies. New in cri(1). New in the Solaris 8

+   -d Check references to data objects. You cannot use -d with

+   -e envar Set the environment variable to envar. This option is useful for experimenting with runtime linker environment variables that can adversely affect ldd itself. New in the Solaris 8

+   -f Force a check for an executable file that is not secure. When ldd is invoked by a super, it does not process any executable that it finds not secure. An executable is considered secure if the interpreter specifies it does not reside in /usr/lib or /etc/lib if the interpreter cannot be determined.

+   -i Display the order of execution of initialization sequences.

+   -l Force the immediate processing of any filters so that all filtered objects and their dependencies are listed.

The immediate processing of filters is the default for ldd starting in the Solaris 8 release. However, under this default, any auxiliary filtered objects that cannot be found are silently ignored. Any missing auxiliary filtered objects generate an error message.

+   -n Enable lazy loading. This mode is the default when the object under inspection is loaded as part of a process. In this case, any dependencies or filters are loaded into the process only when reference is made to a symbol that is defined within the lazy object. You can use the -d or -r options, together with the -l option, to inspect the dependencies and their order of loading because they occur in a running process. New in the Solaris 8 release

+   -r Check references to data objects and functions. You cannot use -r with -d.

+   -s Display the search path to locate object dependencies. When a symbol reference is bound to a dependency, that dependency is deemed used. This option is useful, therefore, only when checking symbol references. If the -r option is not in effect, the -d option is disabled. New in the Solaris 8 release

+   -u Objects that are found to be unused with the -r option should be removed as dependencies. They provide no references but result in unnecessary overhead when filename is loaded. Objects are found to be unused with the -d option when not immediately required when filename is loaded, and they are, therefore, candidates for lazy loading. See "Lazy Loading."