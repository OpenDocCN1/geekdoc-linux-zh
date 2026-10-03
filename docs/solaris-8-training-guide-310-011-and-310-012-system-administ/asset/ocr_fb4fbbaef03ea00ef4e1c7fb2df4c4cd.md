| Field | Description |
|---|---|
| `<profile>` | The name of the class file, a text file that defines how the Solaris software is installed on the system if a system matches the rule. The information in a class file consists of class file keywords and their corresponding class file values. All class files must reside in the JumpStart directory. Class files are described in the section “Creating Class Files.” |
| `<finish>` | The name of an optional Bourne shell script that can be executed after the installation completes. If no finish script exists, you must enter a minus sign (-) in this field. All finish scripts must reside in the JumpStart directory. See the section “Begin and Finish Scripts” for more information. |

The rules file must have the following:

+   - At least one rule
- The name “rules”
- At least a rule keyword, a rule value, and a corresponding profile
- A minus sign (-) in the begin and finish fields if there is no entry

The rules file should be saved in the JumpStart directory, should be owned by root, and should have permissions equal to 644.

The rules file allows the following:

+   - A comment after the pound sign (#) anywhere on a line. If a line begins with a #, the entire line is a comment. If a # is specified in the middle of a line, everything after the # is considered a comment.
- Blank lines.
- Rules to span multiple lines. You can let a rule wrap to a new line, or you can continue a rule on a new line by using a backslash (\ ) before Enter gets pressed.

Table 21.3 describes the various rule_keywords and rule_values that were introduced earlier.