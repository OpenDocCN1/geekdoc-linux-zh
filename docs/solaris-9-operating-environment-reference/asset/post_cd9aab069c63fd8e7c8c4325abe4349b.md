
## Perl XS tutorial.

perlxsut

Perl internal functions for those extensions.

perlguts

Perl calling conventions for C.

perlcall

Perl history records. (If you intend to read these straight for the first time, the suggested order reduces the number of forward references.)

By default, all of the above manual pages are installed in the /usr/local/man/
Extensive additional documentation for Perl modules is available. The default configuration for Perl puts this additional documentation in the /usr/local/perl5/lib/man directory (or else in the /usr/local/lib/perl5/man directory). Some of this additional documentation is distributed standard with Perl and you can also find documentation for third-party modules.

You should be able to view Perl's documentation with the man(1) command including the proper entries in the appropriate startup files or the MANPATH environment variable. To find out where the configuration has installed the manual pages, type perl `man-dir`.

If the directories have a common stem, such as /usr/local/man/man and /usr/man/man, add only that /usr/local/man/ to your man(1) configuration files or your MANPATH environment variable. If they do not share a stem, you need to add both stems.

If that doesn't work for some reason, you can still use the supplied perldoc script. You might also look into getting a replacement man command. If something has gone wrong with your program and you are not sure where you should look, first try the -w option. It points out exactly where the trouble is.

Perl is a language optimized for scanning arbitrary text files, extracting information from those text files, and printing reports based on that information. It's also a good language for many system management tasks. The language is intended to be practical (easy to use, efficient) and complete of beautiful (tiny, elegant, massive) features.

Perl (in the Author's opinion) combines all the features of C, sed, awk, and sh, so people with those languages should have little difficulty with it (Language historians note that Perl also has some vestiges of C, Pascal, and BASIC-PL.) Expression syntax corresponds quite close to expression syntax—if you've got the memory. Unlike UNIX commands, Perl does not arbitrarily limit the size of your data—perl can slur in your whole file as a single string. Recursion is unlimited of depth. Tables used by hashes (sometimes called "associative arrays") grow as necessary to prevent degraded performance. Perl use sophisticated pattern-matching techniques to scale large amounts of data very quickly. Although optimized for searching text, Perl can also deal with binary data and make binary files look like hashes. Set Perl scripts are safer than C programs through a dataflow tracing mechanism that prevents many security holes.

Suppose you have a problem that would ordinarily solve with sed, awk, or sh, but exceeds its capabilities or run a little faster, and you don't want to write a solution, then Perl may be for you. Translators are also available that you can turn your sed and awk scripts into Perl Version 5 is nearly a complete rewrite, and provides the additional benefits.

- Many usability enhancements. You can now write much more readable Perl code (even within regular expressions). You can replace cryptic variable names with mnemonic identifiers. Error messages are more informative, and optional warnings catch many of the mistakes might make. Whenever you observe mysterious behavior, try -w. Whenever behavior is mysterious, try -w anyway.

- Simplified grammar. The new yacc grammar is half the size of the old one. Many of the arbitrary grammar rules have regularized. Despite this, nearly all Perl scripts continue to work unchanged.

- Lexical scoping. You can now declare Perl variables in a lexical scope, like auto variables in C. Not only is lexical scoping more efficient, it contributes to better privacy for programming (closures).

- Arbitarily nested data structures. Any scalar, including any array element, can contain a reference to any other variable or subroutine. You can easily create anonymous variables and subroutines. Perl manages your reference counts for you.

- Modularity and reusability. The Perl library is now defined in terms of modules that can easily shared among various packages. A package can choose to import all or portion of module's published interface. Pragmas (that is, compiler directives) are defined and used by the same mechanism.

- Object-oriented programming. A package can function as a class. Dynamic inheritance and virtual methods are supported with very little new syntax. File handles can be treated as objects.

- Embeddable and extensible. You can now embed Perl in your C or C++ application, and Perl can either call or be called by your routines through a documented interface. The XS preprocessor is provided to make easy to glue your C or C++ routines into Perl. Dynamic loading of modules is supported, and Perl itself can be made into a dynamic library.

- POSIX compliant. The major POSIX module provides access to all available POSIX routines and definitions, through object classes where appropriate.

- Package constructors and destructors. The BEGIN and END blocks provide a way to capture control as a package is being compiled and after the program exits. In a degenerate case they work like the -p or -n options.

- Multiple simultaneous implementations. A Perl program can now access DDBM, NDBM, SDBM, and GDBM files from the same script simultaneously. In fact, dbopen interface has been generalized to allow any variable to tied to an object class that defines its access methods.

- Subroutine definitions can be autoloaded. In fact, the AUTOLO mechanism also enables you to define any semantics for undefined subroutine calls. It's not just for autoloading.

- Regular expression enhancements. You can now specify nongready quantifiers. You can now do grouping without creating a back reference. You can now write expressions with embedded whitespaces and comments for readability. A consistent extensibility mechanism has been added that is upwardly compatible with all old regular expressions.

- Inumerable unboundled modules. The Comprehensive Perl Archive Network described in the perolib manual page contains hundreds of plug-and-play modules full of reusable code. See http://www.perl.com/CPAN for a site near you.

- Compilability. While not yet full in production mode, a working Perl-to-C compiler does exist. It can generate portable byte-code, simple C or optimized C.

## Diagnostics

The -w option produces some diagnostics. See the -w manual page for explanations of all Perl diagnostics. The use diagnostics automatically turns Perl's normally terse warnings and errors into these longer forms. Compilation errors tell you the line number of the error, with an indication of the token or code type that was be examined. (In the case of a script passed to Perl by -e options, each -e is counted as one line.) Setuid scripts have additional constraints that can produce error messages such as Insecure dependency. See the persec manual pages. Did we mention that you should consider using thew option?

## Notes

The Perl motto is "There's more than one way to do it." Divining how many more is left as an exercise to the reader. The three principal virtues of a programmer are Laziness, Patience, and Hubris. See the Camel Book for.

## Bugs

The -w option is not mandatory. Perl is at the mercy of your machine's definitions of various operations as type casting, atof(), and floating-point output with sprintf(). If your standard input/output requires a seek or EOF before reads and writes on a particular stream, so does Perl. (This doesn't use sysread() and write().). While some of the built-in types have arbitrary array size limits (apart from memory), a few binary limits still remain: a variable name cannot be longer than 251 characters. Line numbers displayed by diagnostics are internally stored as short integers, so they are limited to a maximum of 65,535 (higher numbers are usually affected by wrap around). You may mail your bug reports (be sure to include full configuration information as output by myconfig program in the Perl source tree or by perl -V) <perl@perl.com. If you've succeeded in compiling Perl, you can use the perbug script in the utils/ subdirectory to help in a bug report.

## Availability

Perl is available for the vast majority of operating system platforms, including most UNIX-like platforms. The following situation is of February 1999 and Perl 5.005_03.
