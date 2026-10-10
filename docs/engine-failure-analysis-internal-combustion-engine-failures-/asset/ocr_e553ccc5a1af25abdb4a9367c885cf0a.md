# AT A GLANCE (CONT.)

| How Do I | See This Entry | Example |
| --- | --- | --- |
| Search all the files in the working directory for lines containing a specified word and view the matching lines on-screen? | `grep, egrep, fgrep` | `grep "winner" *` |
| Search all the files in the working directory for lines containing a specific word and show just the filenames? | `grep, egrep, fgrep` | `grep -l 'winner' *` |
| Search an entire directory tree for files containing a specified word and show just the filenames? | `grep, egrep, fgrep` | `grep -r1 "winner" /home/suzanne` |
| View the first 10 lines of all the .txt files in the working directory? | `head` | `head *.txt | less` |
| Check the spelling of a text file? | `ispell` | `ispell magic.txt` |
| Quickly find a line in a sorted file that begins with a specified string? | `look` | `look 'Secret #47' secrets.txt` |
| View the status of the printing queue? | `lpq` | `lpq` |
| Print a file using the default print spooler? | `lpr` | `cat example.ps | lpr` |
| Stop printing all of a user’s jobs? | `lprm` | `lprm -` |
| Number the lines in a text file? | `nl` | `nl magic.txt > magic-numbered.txt` |
| Convert a Portable Document Format (PDF) file to PostScript? | `pdf2ps` | `pdf2ps resume.pdf resume.ps` |