% cat datafile
northwest NW Charles Main 3.0 .98 3 34
western WE Sharon Gray 5.3 .97 5 23
southwest SW Lewis Dalsass 2.7 .8 2 18
southern SO Suan Chin 5.1 .95 4 15
southeast SE Patricia Hemenway 4.0 .7 4 17
eastern EA TB Savage 4.4 .84 5 20
northeast NE AM Main Jr. 5.1 .94 3 13
north NO Margot Weber 4.5 .89 5 9
central CT Ann Stephens 5.7 .94 5 13

# EXAMPLE 4.24

```
% grep -v 'Suan Chin' datafile
northwest NW Charles Main 3.0 .98 3 34
western WE Sharon Gray 5.3 .97 5 23
southwest SW Lewis Dalsass 2.7 .8 2 18
southeast SE Patricia Hemenway 4.0 .7 4 17
eastern EA TB Savage 4.4 .84 5 20
northeast NE AM Main Jr. 5.1 .94 3 13
north NO Margot Weber 4.5 .89 5 9
central CT Ann Stephens 5.7 .94 5 13
```

# EXPLANATION

Here, the -v option prints all lines not containing the pattern Suan Chin. This option is used when deleting a specific entry from the input file. To really remove the entry, you would redirect the output of grep to a temporary file, and then change the name of the temporary file back to the name of the original file as shown here:

```
grep -v 'Suan Chin' datafile > temp
mv temp datafile
```

Remember that you must use a temporary file when redirecting the output from datafile. If you redirect from datafile to datafile, the shell will "clobber" the datafile. (See "Redirection" on page 25.)

# EXAMPLE 4.25

```
% grep -l 'SE' .
datafile
datebook
```

# EXPLANATION

The -l option causes grep to print out only the filenames where the pattern is found instead of the line of text.