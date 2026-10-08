# Perl XS tutorial.

perlxsut

Perl internal functions for those extensions.

perlguts

Perl calling conventions for C.

perlcall

Perl history records. (If you intend to read these straight for the first time, the suggested order reduces the number of forward references.)

By default, all of the above manual pages are installed in the /usr/local/man/
Extensive additional documentation for Perl modules is available. The default configuration for Perl puts this additional documentation in the /usr/local/perl5/lib/man directory (or else in the /usr/local/lib/perl5/man directory). Some of this additional documentation is distributed standard with Perl and you can also find documentation for third-party modules

You should be able to view Perl's documentation with the man(1) command including the proper entries in the appropriate startup files or the MANPATH environment variable. To find out where the configuration has installed the manual pages, type perl `man-dir`.

If the directories have a common stem, such as /usr/local/man/man and /usr/man/man, add only that /usr/local/man) to your man(1) configuration files or your MANPATH environment variable. If they do not share a stem, you need to add both stems.

If that doesn't work for some reason, you can still use the supplied perldoc script. You might also look into getting a replacement man command. If something has gone wrong with your program and you are not sure where you should look, first try the -w option. It points out exactly where the trouble is.

Perl is a language optimized for scanning arbitrary text files, extracting information from those text files, and printing reports based on that information. It's also a good language for many system management tasks. The language is intended to be practical (easy to use, efficient) and complete of beautiful (tiny, elegant, massive) features.

Perl (in the Author's opinion) combines all the features of C, sed, awk, and sh, so people with those languages should have little difficulty with it (Language historians note that Perl also has some vestiges of C, Pascal, and BASIC-PL.) Expression syntax corresponds quite close to expression syntax—if you've got the memory. Unlike UNIX commands, Perl does not arbitrarily limit the size of your data—perl can slur in your whole file as a single string. Recursion is unlimited of depth. Tables used by hashes (sometimes called "associative arrays") grow as necessary to prevent degraded performance. Perl use sophisticated pattern-matching techniques to scale large amounts of data very quickly. Although optimized for searching text, Perl can also deal with binary data and make binary files look like hashes. Set Perl scripts are safer than C programs through a dataflow tracing mechanism that prevents many security holes.

Suppose you have a problem that would ordinarily solve with sed, awk, or sh, but it exceeds its capabilities or run a little faster, and you don't want to write a solution, then Perl may be for you. Translators are also available that you can use to turn your sed and awk scripts into Perl.

Perl Version 5 is nearly a complete rewrite, and provides the additional benefits.