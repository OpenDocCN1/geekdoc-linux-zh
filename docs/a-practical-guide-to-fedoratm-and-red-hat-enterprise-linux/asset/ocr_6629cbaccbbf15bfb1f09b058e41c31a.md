# Include
IncludeOptional

Loads directives from files.

`Include \ IncludeOptional` *filename* \ *directory*

where *filename* is the relative pathname of a file that contains directives. Apache prepends ServerRoot (page 955) to *filename*. The directives in *filename* are included in the file holding this directive at the location of the directive. Because *filename* can include wildcards, it can specify more than one file.

The *directory* is the relative pathname that specifies the root of a directory hierarchy that holds files containing directives. Apache prepends ServerRoot to *directory*. The directives in ordinary files in this hierarchy are included in the file holding this directive at the location of the directive. The *directory* can include wildcards.

Whereas Include displays an error when wildcards do not match a file or directory, IncludeOptional does not display an error when there is no match for a wildcard.

The Apache installer puts configuration files for modules, which have a filename extension of conf, in the conf.d and conf.modules.d directories within the ServerRoot directory. The Include directives in the Fedora/RHEL httpd.conf file incorporate module configuration files for whichever modules are installed.

Contexts: server config, virtual host, directory
Default: none
Fedora/RHEL: conf.d/\*.conf conf.modules.d/\*.conf

# LoadModule

Loads a module.

`LoadModule` *module* *filename*

where *module* is the name of an external DSO module and *filename* is the relative pathname of the named module. Apache prepends ServerRoot (page 955) to *filename* and loads the external module specified by this directive. For more information refer to “Modules” on page 968.

Context: server config
Default: none; nothing is loaded by default if this directive is omitted
Fedora/RHEL: loads many modules; refer to the configuration files

# Options

Controls server features by directory.

`Options` [+] *option* [!] *option* ...]

This directive controls which server features are enabled for a directory hierarchy. The directory hierarchy is specified by the container this directive appears in. A + or the absence of a – turns an option on, and a – turns it off.

The *option* might be one of the following:

+   * None—None of the features this directive can control are enabled.
+   * All—All of the features this directive can control are enabled, except for MultiViews, which you must explicitly enable.