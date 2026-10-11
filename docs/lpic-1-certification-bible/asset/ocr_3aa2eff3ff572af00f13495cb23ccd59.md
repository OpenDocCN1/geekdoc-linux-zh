```
# sort nicks >> alphanames
# more alphanames
Peter Anapol
Jeff Arellano
Scott Bessler
Alex Blauvelt
Michael Craig
Joakim Erdfelt
Johannes Erdfelt
Pete Gizzi
David Goolsby
Thomas McCanta
Angie Nash
Jason Nash
Neil Schroeder
Derek Stutman
Paul Ward
Alchemist
Bammage
Dave
Dragonstr
Jackyl
Johan
Just_Joe
Lordram
Netchick
Netjunkie
Pri
Remx-mortis
Sting
Thomas
Zaphod
```

It is also possible to redirect stderr along with stdout. To redirect stderr and stdout to create a new file, you use the >& symbols. For example:

```
sort namelist >& sortednamelist
```

If there are no errors, the contents of the files containing the redirection will appear the same as the contents of the files without the stderr redirection included when there are no errors. However, any errors that occur will be included in these files. The following example is for a file that was created with no errors during processing.

```
# cat sortednamelist
angie
denise
jill
judy
katrina
kim
lisa
monica
nikki
```