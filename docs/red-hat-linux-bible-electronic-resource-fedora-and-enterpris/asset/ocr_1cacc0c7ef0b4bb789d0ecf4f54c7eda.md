# Some useful external programs

Bash is great and has lots of built-in commands, but it usually needs some help to do anything really useful. Some of the most common useful programs you'll see used are `grep`, `cut`, `tr`, and `sed`. Like all the best UNIX tools, most of these programs are designed to work with standard input and standard output, so you can easily use them with pipes and shell scripts.

# The General Regular Expression Parser (*grep*)

The name sounds intimidating, but `grep` is just a way to find patterns in files or text. Think of it as a useful search tool. Getting really good with regular expressions is quite a challenge, but many useful things can be accomplished with just the simplest forms.

For example, you can display a list of all regular user accounts by using `grep` to search for all lines that contain the text /home in the /etc/passwd file as follows:

```
grep /home /etc/passwd
```

Or you could find all environment variables that begin with HO using the following command:

```
env | grep ^HO
```

To find a list of options to use with the `grep` command, type `man grep`.

# Remove sections of lines of text (*cut*)

The `cut` command can extract specific fields from a line of text or from files. It is very useful for parsing system configuration files into easy-to-digest chunks. You can specify the field separator you want to use and the fields you want, or you can break a line up based on bytes.

The following example lists all home directories of users on your system. Using an earlier example of the `grep` command, this line pipes a list of regular users from the /etc/passwd file, then displays the sixth field (-f 6) as delimited by a colon (-d ':').

```
grep /home /etc/passwd | cut -f6 -d ':'
```

# Translate or delete characters (*tr*)

The `tr` command is a character-based translator that can be used to replace one character or set of characters with another or to remove a character from a line of text.

The following example translates all upper-case letters to lowercase letters and displays the words "mixed upper and lower case" as a result:

```
FOO="Mixed UPpEr aNd LoWeR cAsE"
echo $FOO | tr [A-Z] [a-z]
```