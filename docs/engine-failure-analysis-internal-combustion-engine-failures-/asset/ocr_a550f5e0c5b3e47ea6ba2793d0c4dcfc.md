# OPTIONS (CONT.)

**Use This Option**

**To Do This**

**-d, --directory**

Create needed directories and subdirectories when copying and set the file permissions and ownership to the specified settings or to the default settings.

**--help**

Display the available options.

**-g *group name*,**
**--group=*group name***

Set the group ownership of the copied files and directories to the specified group name. You can use the group name or a numeric group ID.

**-o *owner name*,**
**--owner=*owner name***

Set the file ownership of the copied files and directories to the specified owner name. You can use the owner name or a numeric owner ID.

**-m *mode*, --mode=*mode***

Set the permissions of the copied files and directories to the specified mode. You can use octal numbers or symbolic mode specifications (see **chmod** in Chapter 5). The default mode is 0755.

**-p, --preserve-timestamps**

Preserve the source file’s timestamps when copying. By default, the last access and last modification times of the copied files are set to the time of installation.

**-s, --strip**

Remove symbol tables from installed binary executables.

**-S *extension*,**
**--suffix=*extension***

When used with **-b**, apply the specified extension instead of the default backup suffix **~**, which is appended to filenames.

**--version**

Display the version number.

**-V *type*,**
**--version-control=*type***

Specifies the type of backup suffix to use with **-b**. The Available types are as follows:

**t, numbered**	Numbered backups.

**nil, existing**	Numbered if numbered backups exist.