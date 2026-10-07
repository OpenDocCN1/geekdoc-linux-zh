exists. This is necessary since we are appending to the file rather than writing over it. Next, we read the /etc/training_list file by line looking at the fourth field. We compare the letter in the fourth field to determine if it's a C, indicating whether the user is in the C training group. If the letter is a C, we get the name from that line and write it out to the tobetrained file.

# Other Types of Scripts

Although Bash scripts are quite common and can accomplish a lot, there are other types of scripting languages available for Linux. Each of these has its own advantages and disadvantages. This section covers Perl, Python, awk, and sed scripts, although only enough to give you an idea of what these tools can accomplish.

# Perl Scripts

Teaching you the Perl scripting language is not, of course, our intent for this chapter. Rather, we need to prepare you for working with Perl scripts you'll likely run across while performing your Linux system administration duties. To this end, we'll take a brief look at Perl fundamentals to give you the basic familiarity you'll need.

Perl doesn't have a lot of structural requirements. Comments must begin with a pound sign (#), and all lines of code could be written as one line if you wanted it that way. Obviously, white space is irrelevant, meaning reading and maintaining such a program would not be easy, so it's a good idea to use indentation for indicating the script's logical flow.

Perl variables are defined using a statement in this form:

```
$variable = value;
```

To check a variable value, you use two consecutive signs: ==. This is most often done in an statement, a for loop, or a while loop. Perl uses if, for, and while statements the same as Bash shell scripts do:

+   - An if statement compares the value to the variable once and moves on. A simple if statement looks like this:

```
if($variable == 3) {
    print("The value is 3*");
}
```