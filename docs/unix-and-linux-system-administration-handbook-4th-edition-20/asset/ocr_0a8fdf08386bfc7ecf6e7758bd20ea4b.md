# Scripting best practices

Python implements regular expression handling through its re module. No regex features are built into the language itself, so regex-wangling with Python is a bit clunkier than Perl. Here, the regex pattern is initially compiled from the first command-line argument surrounded by parentheses to form a capture group. Strings are then tested and modified with the search and sub methods of the regex object. You can also call search directly as functions, supplying the regex to use the first argument. The \1 in the substitution string is a backreference to the contents of the first capture group.

# 2.6 SCRIPTING BEST PRACTICES

Although the code fragments in this chapter contain few comments and seldom usage messages, that's only because we skeletonized each example to make specific points. Real scripts should behave better. There are whole books on best practices for coding, but here are a few guidelines:

+   - When with inappropriate arguments, scripts should print a usage message and exit. For extra credit, implement --help this way.
- Validate inputs and sanity-check derived values. Before doing a rm -rf on a calculated path, for example, you might have the script double-check that the path conforms to the pattern you expect. You may find your scripting language’s "taint" feature helpful.
- Return an appropriate exit code: zero for success and nonzero for failure. Don't feel compelled to give every failure mode a unique exit code, ever; consider callers will actually want to know.
- Use appropriate naming conventions for variables, scripts, and routines. Conform to the conventions of the language, the rest of your script’s code base, and most importantly, the other variables and functions defined in the current project. Use mixed case or underscores to make long names readable.¹³
- Use variable names that reflect the values they store, but keep them short. number_of_lines_of_input is too long; try n_lines.
- Consider developing a style that you and your colleagues agree on to the same conventions. It makes it easy for you to read other people’s code and for them to read yours.
- Start every script with a comment block that tells what the script does and what parameters it takes. Include your name and the date. If the script requires nonstandard tools, libraries, or modules to be installed on the system, list those as well.

> 13. The naming of the scripts themselves is important, too. In this context, dashes are more common than underscores for simulating spaces, as in system-config-parser.