# Exercises

+   1. Assume a program accepts options -a, -b, and -c, and that -b requires an argument. Write the manual argument parsing code for this program, without using `getopt()` or `getopt_long()`. Accept `--` to end option processing. Make sure that -ac works, as do -byYANKEES, -b YANKEES, and -abyYANKEES. Test your program.

+   2. Implement `getopt()`. For the first version, don't worry about the case in which `optstring[0] == ':'`. You may also ignore `opterr`.

+   3. Add code for `optstring[0] == ':'` and `opterr` to your version of `getopt()`.

+   4. Print and read the GNU `getopt.h`, `getopt.c` and `getoptl.c` files.

+   5. Write a program that declares both `environ` and `envp` and compares their values.

+   6. Parsing command line arguments and options is a wheel that many people can't refrain from reinventing. Besides `getopt()` and `getopt_long()`, you may wish to examine different argument-parsing packages, such as:

+   - The *Plan 9 From Bell Labs* `arg(2)` argument-parsing library,⁴
+   - `Arnp`,⁵
+   - `Argv`,⁶
+   - `Autoopts`,⁷
+   - GNU `Gengetopt`,⁸
+   - `Opt`,⁹
+   - `PoP`.¹⁰ See also the *pop(3)* manpage on a GNU/Linux system.

+   7. Extra credit: Why can't a C compiler completely ignore the `register` keyword? Hint: What operation *cannot* be applied to a `register` variable?

+   ⁴ http://plan9.bell-labs.com/magic/man2html/2/arg
+   ⁵ http://www.gnu.org/manual/glibc/html_node/Argp.html
+   ⁶ http://256.com/sources/argv
+   ⁷ http://autoogen.sourceforge.net/autoopts.html
+   ⁸ ftp://ftp.gnu.org/gnu/gengetopt/
+   ⁹ http://niss-www.lanl.gov/~jt/Software/opt/opt-3.19.tar.gz
+   ¹⁰ http://freshmeat.net/projects/popt/7topic_id=809