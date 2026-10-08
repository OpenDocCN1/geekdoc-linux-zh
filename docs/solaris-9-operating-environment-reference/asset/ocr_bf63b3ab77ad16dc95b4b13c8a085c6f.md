# make 789

concatenation of those files, in order of appearance. (See also . .KEEP_STATE and .KEEP_STATE_FILE in "Special-Function Targets" on page 793).

Print commands, but do not execute them. Print lines beginning with an @ However, if a command line contains a reference to the $ (MAKE) macro, always execute that line (the discussion of MAKEFLAGS in "Reading Makefiles and the Environment" on page 789). When in POSIX mode, execute lines beginning with a (+).

+   -n

Print the complete set of macro definitions and target descriptions.

+   -p

Merely report dependencies instead of building them.

+   -P

Return a 0 non-zero status code depending on whether the target file is up-to-date. When in POSIX mode, execute lines beginning with a plus (+).

+   -r

Do not read the default Makefile /usr/share/lib/make/make.rules.

+   -s

Do not print command lines before executing them. Equivalent to the special function SILENT.

+   -S

Undo the effect of the -k option. Stop processing when a command returns a non-zero exit status.

+   -t

Touch the target (bringing them-to-date) instead of performing their rules. This option can be dangerous when files are maintained by more than one person. When the .KEEP_STATE appears in the Makefile, update the target file just as if the rules had been performed. When in POSIX mode, execute lines beginning with a (+).

+   -V

Put make into SysV mode. Refer to sysmake(1) for details.

# Operands

target

Target names.

macro=value

Macro definition. This definition overrides any regular definition for the specified macro within the Makefile itself or in the environment. However, you can override this definition with conditional macro assignments.

# Usage

Refer to make in Programming Utilities Guide for tutorial information.

# Reading Makefiles and the Environment

When make starts, it reads the MAKEFLAGS environment variable to obtain any of the following options specified in value: -d, -D, -e, -i, -k, -n, -p, -q, -r, -s, -S, or -t. Because of the implementation of POSIX.2 (see POSIX.2(5), the MAKEFLAGS values