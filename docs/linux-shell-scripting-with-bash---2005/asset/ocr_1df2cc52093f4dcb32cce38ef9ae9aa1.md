For example, if the param2.sh script expects -n (help) and -c (company ID) with a company ID argument, the OPTSTRING would be hc::.

There is a second required parameter after the list of options: The name of a shell variable into which to record each option encountered.

Each time the getopts command runs, the next switch on the command line is examined and the name of the switch is saved in the variable SWITCH. The position of the next parameter to be examined is in a variable called OPTIND. If it doesn't exist, OPTIND automatically set to 1 before the first script parameter is checked. If there is any argument to the script, it is saved in a variable called OPTARG. Listing 9.3 shows a short script that tests the first parameter of the script.

# Listing 9.3 getopt.sh

```
```
#!/bin/bash
#
# getopt.sh



declare SWITCH
getopts "hc:" SWITCH
printf "The first switch is SWITCH=%s OPTARG=%s OPTIND=%s\n" \\
    "$SWITCH" "$OPTARG" "$OPTIND"
```
```

In this short script, unknown switches assign a question mark (? ) to the SWITCH variable; an error message is displayed.

```
```
$ bash getopt.sh -h
The first switch is SWITCH=h OPTARG= OPTIND=2
$ bash getopt.sh -c a4327
The first switch is SWITCH=c OPTARG=a4327 OPTIND=3
$ bash getopt.sh -a
t.sh: illegal option -- a
The first switch is SWITCH=? OPTARG= OPTIND=1
```
```

The error message can be hidden using a colon as the first character in the switch list. By using :hc:: the error on the bad switch -a disappears, but the bad option is saved in OPTARG to be used in a custom error message.

```
```
$ bash getopt.sh -a
The first switch is SWITCH=? OPTARG=a OPTIND=1
```
```

You can also hide errors by creating an OPTERR variable with the value of 0. This overrides the contents of the legal switches string.

Switches are usually checked with a while and case statement. See Listing 9.4.

# Listing 9.4 getopt_demo.sh

```
```
# getopt_demo.sh
#
```
```