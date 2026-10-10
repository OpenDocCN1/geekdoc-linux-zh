```
```
First Data Line
Header Line
$
```
```

Now you can easily use the sed editor script on any file without having to constantly retype the entire sed command line.

# ## Redirecting sed output

By default, the sed editor outputs the results of the script to STDOUT . You can employ all the standard methods of redirecting the output of the sed editor in your shell scripts.

You can use dollar sign/parenthesis, $() , to redirect the output of your sed editor command to a variable for use later in the script. The following is an example of using the sed script to add commas to the result of a numeric computation:

```
```
$ cat fact.sh
#!/bin/bash
# Shell wrapper for sed editor script
# to calculate a factorial, and
# format the result with commas.
#
factorial=1
counter=1
number=$1
#
# while [ $counter -le $number ]
do
    factorial=$[ $factorial * $counter ]
    counter=$[ $counter + 1 ]
done
#
result=$(echo $factorial | sed '{
:start
s/^\(.\*[0-9]\)\([0-9]\{3}\}\)/\1,\2/
t start
}')
# echo "The result is $result"
#
exit
$ ./fact.sh 20
```
```