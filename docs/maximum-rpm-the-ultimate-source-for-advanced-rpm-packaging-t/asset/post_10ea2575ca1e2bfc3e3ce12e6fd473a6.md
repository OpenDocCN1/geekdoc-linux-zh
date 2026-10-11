
What does all this stuff mean? Let’s go through it, item by item:

- /usr/sbin/adduser is simple: It’s the name of the file being dumped.
- 4442 is the size of the file, in bytes.
- How about 841083888? It’s the time the file was last modified, in seconds past the UNIX zero date of January 1, 1970.
- ca5fa53dc74952aa5b5e3a5fa5d8904b is the MD5 checksum of the file’s contents, all 128 bits of it.
- If you guessed 0100755 was the file’s mode, you were right.
- The first root represents the file’s owner.
- The second root is the file’s group.
- We’ll take the next part (0 0) in one chunk. The first 0 shows whether the file is a config file. If 0, as in this case, the file is not a config file. The next 0 shows whether the file is documentation. Again, since there is a 0 here, this file isn’t documentation either.
- The final 0 represents the file’s major and minor numbers. These are set only for device special files. Otherwise, it will be 0.
- If the file were a symlink, the spot taken by X would contain a path pointing to the linked file.

Normally, the --dump option is used by people who want to extract the file-related information from RPM and process it somehow.

### 5.2.2.10. --scripts: Show Scripts Associated with a Package

If you add --scripts (that’s two dashes) to a query, you get to see a little bit more of RPM’s underlying magic:

```bash
# rpm -q --scripts XFree86
preinstall script:
(none)

postinstall script:
/sbin/ldconfig
/sbin/pamconfig --add --service=xdm --password=none --sesslist=none

preuninstall script:
(none)

postuninstall script:
/sbin/ldconfig
if [ "$1" = 0 ]; then
/sbin/pamconfig --remove --service=xdm --password=none --sesslist=none
fi

verify script:
(none)
#
```

In this particular case, the XFree86 package has two scripts: One labeled postinstall and one labeled postuninstall. As you might imagine, the postinstall script is executed just after the package's files have been installed; the postuninstall script is executed just after the package's files have been erased.

Based on the labels in this example, you'd probably imagine that a package can have as many as five different scripts. You'd be right:

- The preinstall script, which is executed just before the package's files are installed.
- The postinstall script, which is executed just after the package's files are installed.
- The preuninstall script, which is executed just before the package's files are removed.
- The postuninstall script, which is executed just after the package's files are removed.
- And finally, the verify script. While it's easy to figure out the other scripts' functions based on their name, what does a script called verify do? Well, we haven't gotten to it yet, but packages can also be verified for proper installation. This script is used during verification. (For more information on package verification, see section 6.1 in Chapter 6, "Using RPM to Verify Installed Packages.")

Is this something you'll need very often? As in the case of displaying file states, not really. But when you need it, you really need it!

### 5.2.2.11. --queryformat: Construct a Custom Query Response

Okay, say you're still not satisfied. You'd like some additional information, or you think a different format would be easier on the eyes. Maybe you want to take some information on the packages you've installed and run it through a script for some specialized processing. You can do it, using the --queryformat option. In fact, if you look back at the output of the -l option, you'll notice that RPM was using --queryformat internally. Here's how it works: On the RPM command line, include --queryformat. Right after that, enter a format string, enclosed in single quotes (').

The format string can consist of a number of different components:

- Literal text, including escape sequences
- Tags, with optional field width, formatting, and iteration information
- Array iterators

Let's look at each of these components.

#### 5.2.2.11.1. Literal Text

Any part of a format string that is not associated with tags or array iterators will be treated as literal text. Literal text is just that: It’s text that is printed just as it appears in the format string. In fact, a format string can consist of nothing but literal text, although the output wouldn’t tell us much about the packages being queried. Let’s give the `--queryformat` option a try, using a format string with nothing but literal text:

```bash
# rpm -q --queryformat 'This is a test!' rpm
This is a test!#
```

The `RPM` command might look a little unusual, but if you take out the `--queryformat` option, along with its format string, you’ll see that this is just an ordinary query of the `rpm` package. When the `--queryformat` option is present, `RPM` will use the text immediately following the option as a format string. In this case, the format string is 'This is a test!'. The single quotes are required. Otherwise, it’s likely that your shell will complain about some of the characters contained in the average format string.

The output of this command appears on the second line. As you can see, the literal text from the format string was printed exactly as it was entered.

#### 5.2.2.11.2. Carriage Control Escape Sequences

Wait a minute. What is that `#` doing at the end of the output? Well, that’s our shell prompt. You see, we didn’t direct `RPM` to move to a new line after producing the output, so the shell prompt ended up being tacked to the end of the output.

Is there a way to fix that? Yes, there is. We need to use an escape sequence. An escape sequence is a sequence of characters that starts with a backslash (`\`). Escape sequences add carriage control information to a format string. The following escape sequences can be used:

- `\a`—Produces a bell sound or similar alert.
- `\b`—Backspaces one character.
- `\f`—Outputs a form-feed character.
- `\n`—Outputs a newline character sequence.
- `\r`—Outputs a carriage return character.
- `\t`—Causes a horizontal tab.
- `\v`—Causes a vertical tab.
- `\\`—Displays a backslash character.

Based on this list, it seems that an `\n` escape sequence at the end of the format string will put our shell prompt on the next line:

```bash
# rpm -q -queryformat 'This is a test!\n' rpm
This is a test!
#
```

Much better.

#### 5.2.2.11.3. Tags

The most important parts of a format string are the tags. Each tag specifies what information is to be displayed and can optionally include field width, as well as justification and data formatting instructions. (RPM uses printf to do --queryformat formatting. Therefore, you can use any of the printf format modifiers discussed in the printf(3) man page.)

But for now, let’s look at the basic tag. In fact, let’s look at three: the tags that print the package name, version, and release. Strangely enough, these tags are called NAME, VERSION, and RELEASE. In order to be used in a format string, the tag names must be enclosed in curly braces and preceded by a percent sign. Let’s give it a try:

```bash
# rpm -q --queryformat '%{NAME}%{VERSION}%{RELEASE}\n' rpm
# rpm-2.3.1
#
```

Let’s add a dash between the tags and see if that makes the output a little easier to read:

```bash
# rpm -q --queryformat '%{NAME}-%{VERSION}-%{RELEASE}\n' rpm
# rpm-2.3-1
#
```

Now our format string outputs standard package labels.

#### 5.2.2.11.4. Field Width and Justification

Sometimes it’s desirable to allocate fields of a particular size for a tag. This is done by putting the desired field width between the tag’s leading percent sign and the opening curly brace. Using our package-label-producing format string, let’s allocate a 20-character field for the version:

```bash
# rpm -q --queryformat '%{NAME}-%20{VERSION}-%{RELEASE}\n' rpm
# rpm-
             2.3-1
#
```

The result is a field of 20 characters: 17 spaces followed by the 3 characters that make up the version.

In this case the version field is right-justified; that is, the data is printed at the far right of the output field. We can left-justify the field by preceding the field width specification with a dash:

```bash
# rpm -q --queryformat '%{NAME}--20{VERSION}-%{RELEASE}\n' rpm
# rpm-2.3
         -1
#
```

Now the version is printed at the far left of the output field. You might be wondering what would happen if the field width specification didn’t leave enough room for the data being printed. The field width specification can be considered the minimum width the field will take. If the data being printed is wider, the field will expand to accommodate the data.

#### 5.2.2.11.5. Modifiers—Making Data More Readable

While RPM does its best to appropriately display the data from a --queryformat, there are times when you’ll need to lend a helping hand. Here’s an example. Say we want to display the name
