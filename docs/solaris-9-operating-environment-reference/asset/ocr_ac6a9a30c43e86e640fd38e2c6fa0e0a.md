# awk

# 893

assignment operand that begins with an underscore alphanumeric character from the portable character set, followed by a sequence of underscores, digits, and alphabetics from the portable character set, the = character specifies a variable assignment instead of a path name. The characters before the = represent the name of a awk variable; if name is a awk reserved word, the behavior is undefined. The characters following the equal sign are interpreted as if they appeared in the awk program preceded and followed by a double-quote (") character, as a STRING token. When the last character is an unescaped backslash, it is interpreted as a literal backslash instead of the first character of the sequence ". The variable is assigned the value of that STRING token. The value is considered a numeric string, the variable is assigned its numeric value. Each such assignment is performed just before the processing of the following file (if any). Thus, an assignment before the first file argument is executed after the BEGIN actions (if any), whereas an assignment after the file argument is executed before the END actions (if any). If there are no file arguments, execute assignments before processing the standard input.

# Input Files

Input files to the awk program can come from any of the following sources:

+   - Any file operands or their equivalents, achieved by modifying the awk variables ARV and ARGC.
- Standard in input in the absence of any file operands.
- Text file arguments to the getline function. Whether the variable RS is set to a value other than a new character, for these files, implementations support records terminated with the specified separator up to {LINE_MAX} bytes and can support longer records.
- Text file arguments to the -f profile option containing a awk program.
- The standard input when you specify no file operands or if file operand is -.

# Extended Description

A awk program is composed of pairs of the form:
pattern ( action )

You can omit either the pattern or the action, including the brace characters. Separate pattern-action statements by a semicolon or by a newline.

A missing pattern matches any record of input, and a missing action is equivalent to an action that matches the matched record of input to standard output.
Execution of the awk program is done as follows.