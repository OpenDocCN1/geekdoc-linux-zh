The directory /etc/apparmor.d/abstractions/ contains files with general rules grouped by common application tasks. These include, for instance, access to files all applications need (base), access to authentication mechanisms (authentication), graphics environments (kde, gnome), name resolution (nameservice), and others. Instead of having these redundantly specified in several profiles, they are defined at one point and included in the profiles that need them.

Line 5 in the example above gives the absolute path to the program confined by AppArmor. The rules as well as any includes follow within the curly braces {}.

Line 8 enables the capability sys_admin for this program. Any other capabilities needed would be listed in separate lines starting with capability.

The remaining lines list files and directories, and the access permission granted.

Within lines listing files and directories, the following wildcards can be used:

+   - *. Substitutes any number of characters, except /.
+   - **. Substitutes any number of characters, including /. Use ** to include subdirectories.
+   - ?. Substitutes any single character, except /.
+   - [abc]. Substitutes a, b, or c.
+   - [a-d]. Substitutes a, b, c, or d.
+   - {ab,cd}. Substitutes either ab or cd.

The permissions granted can be

+   - r. Allows the program to have read access to the resource. Read access is required for scripts, and an executing process needs this permission to allow it to dump core or to be attached to with ptrace.