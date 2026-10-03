# TABLE 21.4

# CHECK SCRIPT OPTIONS

| Option | Description |
|---|---|
| -p `<path>` | Validates the rules file by using the check script from a specified Solaris 8 CD image, instead of the check script from the system you are using. `<path>` is the pathname to a Solaris installation image on a local disk or a mounted Solaris CD. Use this option to run the most recent version to see if your system is running a previous version of Solaris. |
| -r `<file_name>` | Specifies a rules file other than a file named “rules.” Using this option, you can test the validity of a rule before integrating it into the rules file. With this option, a rules.ok file is not created. |

When you use check to validate a rules file, the following things happen:

+   1. The rules file is checked for syntax. check makes sure that the rule keywords are legitimate, and the `<begin>`, `<class>`, and `<finish>` fields are specified for each rule.
2. If no errors are found in the rules file, each class file specified in the rules file is checked for syntax.
3. If no errors are found, check creates the rules.ok file from the rules file, removing all comments and blank lines, retaining all the rules, and adding the following comment line to the end:
`version=2 checksum=<num>`

As the check script runs, it reports that it is checking the validity of the rules file and the validity of each class file. If no errors are encountered, it reports the following:

```
The custom JumpStart configuration is ok.
```

The following is a sample session that uses check to validate a rules and class file. I named the rules file “rulestest” temporarily, the class file is named “basic_prof,” and I am using the -r option. With -r, the rules.ok file is not created, and only the rulestest file is checked.

```
#/export/jumpstart/install/Solaris_8/Misc/jumpstart_sample/ \
check -r /tmp/rulestest
Validating /tmp/rulestest...
Validating profile basic_prof...
```