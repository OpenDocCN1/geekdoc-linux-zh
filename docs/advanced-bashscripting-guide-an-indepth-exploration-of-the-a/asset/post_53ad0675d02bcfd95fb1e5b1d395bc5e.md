
# Advanced Bash–Scripting Guide

- For more detail on burning CDRs, see Alex Withers' article, Creating CDs, in the October, 1999 issue of [Linux Journal.]

- The -c option to mke2fs also invokes a check for bad blocks.

- Operators of single-user Linux systems generally prefer simpler tools for backups, such as tar.

- NAND is the logic "not–and" operator. Its effect is somewhat similar to subtraction.

- For purposes of command substitution, a command may be an external system command, an internal scripting builtin, or even a script function.

- A descriptor is simply a number that the operating system assigns to an open file to keep track of it. Or considered a simpler version of a file pointer. It is analogous to a file handle in C.

- Using file descriptor 5 might cause problems. When Bash creates a child process, as exec, the child inherits fd 5 (see Chet Cheney's e-mail, SUBJECT: RE: File descriptor 5 is held open). Best leave particular fd alone.

- The simplest type of Regular Expression is a character string that retains its literal, not containing any metacharacters.

- Since sed, awk, grep process single lines, will usually not match a newline. In those cases where there is a newline in a multiple line expression, the dot will match the newline.

```bash
#!/bin/bash
sed -e 'N;s/\n/\n/ ' << EOF # Here Document
line1
line2
EOF
# OUTPUT:
# [line1]
# line2

echo
awk '{ $0~"\n" $2; if (./line.1/) (print)' << EOF
line 1
line 2
EOF
# OUTPUT:
# line
#

 Thanks, S.C.
exit 0
```

- Filename expansion can match dotfiles, but only if the pattern explicitly includes the dot.

## Appendix J. Copyright

```
~/[.bashrc      # Will not expand to ~/.bashrc
~/.bashrc       # Neither this.
               # Wild cards and metacharacters will not expand to a dot in globbing.

~/.[b]ashrc      # Will expand to ~/.bashrc
~/.ba7rc       # Likewise.
~/.bash*       # Likewise.
```

# Setting the "globopt option turns this off.

# Thanks, S.C.

- This has the effect as a named pipe (temp file), and, in fact, named pipes were at time used in process substitution.

- Indirect variable references (see Example 35–2) provide a clumsy sort of mechanism for passing variable pointers to functions.

# Thanks to Stephanie Chazelas for providing this instructive example.

exit 0

- The return command is a Bash builtin.

- Herbert Mayer defines recursion as "...expressing an algorithm by using a simpler version of that same algorithm..." A recursive function is one that calls itself.

## Appendix J. Copyright

- Too many levels of recursion may crash a script with segfault.

```bash
#!/bin/bash
recursive_function ()
{
  (( $1 < $2 )) && f $(( $1 + 1 )) $2;
  # As long as 1st parameter is less than 2nd,
  # increment 1 and recurse.
}

recursive_function 1 50000 # Recursion 50,000 levels!
# Segfaults, of course.

# Recursion this deep might cause a C program to segfault
# by using up all the memory allotted to the stack.

# Thanks, S.C.
exit 0 # This script will not exit normally.
```

- However, aliases seem to expand positional parameters.

- This does not apply to csh, tsh, and others not related to or descended from the classic Bourne shell (sh).

- The entries in /dev provide mount points for physical and virtual devices. These entries take very little drive space.

- Some devices, as /dev/null, /dev/zero, and /dev/urandom are virtual. They are not actual physical devices and exist only in software.

- A block device reads and/or writes data in chunks or blocks, in contrast to a character device, which accesses data in character units. Examples of block devices are a hard drive and CD ROM drive. An example of a character device is a keyboard.

- Certain system commands, such as procinfo, free, vmstat, lsdev, and uptime do this as well.

- By convention, signal 0 is assigned to exit.

- Setting the su permission on a script has no effect.

- In this context, "magic numbers" have an entirely different meaning than the magic numbers used to designate file types.

- Chet Ramey promises associative arrays (a Perl feature) in a future Bash release.

- Those who can, do; who can't... get an MCSE.

- If no address range is specified, the default is all lines.

- *

## Appendix J. Copyright

# Advanced Bash–Scripting Guide

- Out of range exit values can result in unpredictable exit codes. For example, **exit 3809** gives an exit code of 225.
