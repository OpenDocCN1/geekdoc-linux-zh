# $ ./hash2.pl
Keys: boat 4 number five
Values: tuna fish 5

Perl automatically quotes a single word that appears to be the left of the =
operator, you do not need quotation marks around board in the third line of this program. However, removing the quotation marks from around number five would
generate an error because the string contains a SPACE.

# Control Structures

Control flow statements alter the order of execution of statements within a Perl program. Starting on page 954, Chapter 27 discusses bash structures in detail and includes flow diagrams. Perl control structures perform the same functions as bash counterparts, although the two languages use different syntaxes. The description of each control structure in this section references the discussion of the same control structure under bash.

In this section, the bold italic in the description are the items you use to cause the syntax to have the desired effect, the nonbold italic words are the keywords Perl uses to identify the control structure, and [...] represents a block (page 1045) of statements. Many of these structures use an expression, denoted as expr, to control their execution. if/unless (next) for an example and explanation of a syntax description.

# if/unless

The and unless control structures are compound statements that have the following
syntax:

+   - if (expr) [...]

+   - unless (expr) [...]

These structures differ only in the sense of the test they perform. The if structure executes the block of statements if expr evaluates to true; unless executes the block of statements unless expr evaluates to true (i.e., if expr is false).

The appears in nonbold type because it is a keyword; The expr is an expression; Perl evaluates and executes the block (page 1045) of statements represented by [...] if the expression evaluates as required by the control structure.

The expr in the following example, -r memo, uses the -r file operator to determine if a file named memo exists in the directory and if the file is readable. Although this operator only tests whether you have read permission for the file, the file must exist for you have read permission; thus it implicitly tests that the file is present (Perl uses the same file test operators as bash; Table 27-1 on page 957.). If this expression evaluates to true, Perl executes the

File test operators