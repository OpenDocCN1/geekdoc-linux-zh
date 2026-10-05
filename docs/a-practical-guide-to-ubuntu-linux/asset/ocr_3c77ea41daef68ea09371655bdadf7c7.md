# INTRODUCTION TO PERL 1045

# TERMINOLOGY

This section defines some of the terms used in this chapter.

Module A Perl module is a self-contained chunk of Perl code, frequently containing several functions that work together. A module can be called from another module or from a Perl program. A module must have a unique name. To help ensure names, Perl provides a hierarchical namespace (page 1161) for modules, separating components of a name with double colons (::). Example names are Timestamp::Simple and WWW::Mechanize.

Distribution A Perl distribution is set of one or more modules that perform a task. You can search for distributions and methods at search.cpan.org. Examples of distributions including Timestamp-Simple (the Timestamp-Simple-1.01.tar.gz archive file contains the Timestamp::Simple (simple module only) and WWW-Mechanize (WWW-Mechanize-1.34.tar.gz contains the WWW::Mechanize module, plus supporting modules including WWW::Mechanize::Link and WWW::Mechanize::Image)

Package A package defines a Perl name. For example, in the variable with the name WWW::Mechanize::ex, is a scalar variable in the WWW::Mechanize package, where “package” is used in the sense of a namespace. Using the same name, as WWW::Mechanize, for a distribution, a package, and can be confusing.

Block A block is zero or more statements, defined by curly braces ({}), that defines a scope. The shell control syntax explanations refer to these elements as commands. See the if...then control structure on page 954 for an example.

Variable A package variable is defined within the package it appears in. Other packages refer to package variables by using the variable's fully qualified name (for example, SText::Wrap::columns). By default, variables unless define them as lexical variables.

Lexical A lexical variable, which is defined by the name of a variable with the keyword my (see the tip on page 1050), is defined only within the block or file it appears in. Other languages refer to lexical variable as a local variable. Because Perl 4 used the lexical keyword with a different name, Perl 5 uses the lexical in in its place. When programming bash, variables that are not exported (page 992)

+   List A list is a series of zero or more scalars. The following list has three elements—two numbers and a string:

(2, 4, 'Zach')

Array An array is a variable that holds a list of elements in a defined order. The following line of code, @a is an array. See page 1053 for information about array variables.

```
@a = (2, 4, 'Zach')
```

Compound A compound statement is made up of other statements. For example, if the if statement (page 1057) incorporates an statement that normally includes other statements within the block it controls.