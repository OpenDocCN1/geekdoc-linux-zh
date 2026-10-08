not shown by default, and the user must request to see them at the shell prompt.
In this case, they can be viewed by using the all option for ls.
The command would then be seen as follows:

```
> ls -all /
total 12
```

You can see the difference in the two examples; one shows all twelve files, and the other shows ten files and hides the other.

Now that you are comfortable using the ls command, you should know that Unix has many options for expanding on the ls command in addition to the ones discussed here. For example, options for sorting, for tabulating data, and for adding flags to a “short” listing to show a file’s attributes can also be used with the ls command. Beyond the -l and -a options discussed previously, some other options that you are likely to come across include the following:


+   - -F option: Option is used to indicate file attributes.
- -R option: This option is used to recursively list all files below a specified directory.

> Don't Forget Case Sensitivity When using arguments such as the ones you just listed, you will need to take note of whether they are in uppercase or lowercase. Remember that performing the wrong command in Unix can be damaging because there are few checks implemented to keep you safe from yourself. Make sure you use the help system if you are unsure about what switches you need to define to achieve specific actions.

That wasn't so bad, was it? Now, you can log in to Unix, get help if needed, perform basic navigation, see where you are logging into Unix for the first time, and see what contents are contained within items in your path. If this is your first time doing these things and you were successful, you should be proud of how far you have gotten in such a