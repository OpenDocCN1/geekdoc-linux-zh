The training script in Listing 17.5 first declares its command interpreter to be the shell /bin/bash. Next, the script removes the toberained file in the user’s directory if one exists. This is necessary since we are appending to the file rather than writing over it. Next, we read the /etc/training_list file line by line looking at the fourth field. We compare the letter in the fourth field to determine if it’s a C, indicating whether the user is in the C training group. If the letter is a C, we get the name from that line and write it out to the toberained file. In large companies, the training_list would probably be a MySQL database instead of a flat file, but the basic idea would be the same.

# # Other Types of Scripts

Although Bash shell scripts are quite common and can accomplish a lot, there are other types of scripting languages available for Linux. Each of these has its own advantages and disadvantages. This section covers Perl, Python, awk, and sed scripts, although only enough to give you an idea of what these tools can accomplish.

# ## Perl Scripts

Teaching you the Perl scripting language is not, of course, our intent for this chapter. Rather, we want to prepare you for working with Perl scripts you’ll likely run across while performing your Linux system administration duties. To this end, we’ll take a brief look at Perl fundamentals to give you the basic familiarity you’ll need.

Perl doesn’t have a lot of structural requirements. Comments must begin with a pound sign (#), and all lines of code end in a semicolon. White space is irrelevant, meaning that the entire program could be written as one line if you wanted it that way. Obviously, reading and maintaining such a program would not be easy, so it’s a good idea to use indentation for indicating the script’s logical flow.

Perl variables are defined using a statement in this form:

```
```Perl
$variable = value;
```
```

To check a variable’s value, you use two consecutive equal signs: ==. This is most often done in an if statement, a for loop, or a while loop. Perl uses if, for, and while statements much the same as Bash shell scripts do:

+   - An if statement compares the value to the variable once and then moves on. A simple if statement looks like this:

```
```Perl
if ($variable == 3) {
    print ("The value is 3");
}
```
```

+   - A for loop cycles through a number of values comparing them to a variable or a constant. When the list has been exhausted, the loop ends. A simple for loop looks like this:

```
```Perl
#set the maximum length to 0
$maxLength= 0 ;

#cycle through each length and compare it to the maxLength
foreach (keys %in) {
    $maxLength= length if length > $maxLength ;
}

#increment the maxLength variable
$maxLength++ ;
```
```