# Looking at the Template

We here a numbered list of the finished template.

```
```bash
1 #!/usr/bin/env bash
2 #
3 # new_script-demo - Demonstrate the new_script template
4
5 # Copyright 2021, Linux User <me@linuxbox.example.com>
6 # This program is free software: you can redistribute it and/modify
7 # it under the terms of the GNU General Public License as published by
8 # the Free Software Foundation, either version 3 of the License, or
9 # (at your option) any version.

10 # This program is distributed in the hope that it will be useful,
11 # WITHOUT ANY WARRANTY; even the implied warranty of
12 # MERCHANTABILITY OR FITNESS FOR A PARTICULAR PURPOSE. See the
13 # GNU General Public License at <http://www.gnu.org/licenses/> for
14 # more details.

15 # Usage: new_script-demo [-h|--help]
16 # new_script-demo [-a|--option_a] [-b|--option_b_argument]

17 # Revision history:
18 # 2021-05-05 Created by new_script version 3.5.3
19
```
```

The comment block is complete with license, usage, and revision history. Notice the first letter of the purpose has been capitalized. new_script gets the author's name from /etc/password file and email address have been calculated. If the REPLOY variable is set, it supplies the email address (this was common with old-time programs); otherwise the email address will be expanded from $USER$(hostname). To define the REPLOY variable, we just add it to our
~/.bashrc file.

```
export REPLOY=me@linuxbox.example.com
```

Our script template contains the constants and with functions:

```
```bash
20 PRONAME=$(basename $0)
21 VERSION="0.1"
22 LIBS= # Insert pathnames of required external shell libraries here
```
```

The global constants appear with the program name (derived from $0) and the version number. The LIBS constant should be set to contain a space-delimited list (in double quotes of course) of any files to be sourced. Note: the template implements this feature requires library pathnames do not contain spaces. Besides the template not working, including embedded spaces in a library name would be extremely poor taste.

```
```bash
23 clean_up() {
24 # Perform pre-exit housekeeping
25   return
26 }
```
```

# 214 Coding Standards Part 2: new_script