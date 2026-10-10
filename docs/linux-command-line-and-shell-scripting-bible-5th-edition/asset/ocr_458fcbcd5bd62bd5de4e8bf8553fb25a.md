The shell script called `reverse.sh` uses the `sed` editor script to reverse text lines in a data stream. It uses the `$1` shell parameter to retrieve the first parameter from the command line, which should be the name of the file to reverse:

```
`$ cat data2.txt`
Header Line
First Data Line
Second Data Line
End of Data Lines
$
`$ ./reverse.sh data2.txt`
End of Data Lines
Second Data Line
First Data Line
Header Line
$
```

Now you can easily use the `sed` editor script on any file without having to constantly retype the entire `sed` command line.

# Redirecting `sed` output

By default, the `sed` editor outputs the results of the script to STDOUT. You can employ all the standard methods of redirecting the output of the `sed` editor in your shell scripts.

You can use dollar sign/parentheses, `$( )`, to redirect the output of your `sed` editor command to a variable for use later in the script. The following is an example of using the `sed` script to add commas to the result of a numeric computation:

```
`$ cat fact.sh`
`#!/bin/bash`
`# Shell wrapper for sed editor script`
`# to calculate a factorial, and`
`# format the result with commas.`
`#`
`factorial=1`
`counter=1`
`number=$1`
`#`
`while [ $counter -le $number ]`
`do`
`    factorial=$( $factorial * $counter )`
`    counter=$( $counter + 1 )`
`done`
`#`
`result=$(echo $factorial |`
`sed '{`
`:start`
`s/\(.\{0-9\}\\{0-9}\{3\}\\)\(.\{2\}`
`t start`
```