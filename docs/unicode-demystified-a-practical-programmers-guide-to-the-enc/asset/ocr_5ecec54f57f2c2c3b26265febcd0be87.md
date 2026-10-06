The fc builtin can take zero, one, or two arguments with the -l option. The arguments specify a part of the history list to be displayed. The syntax is

```
fc -l [first | [last]]
```

The fc builtin lists commands beginning with the most recent event that matches the first argument. The argument is the number of the event, the first few characters of the command line, or a negative number, which is taken to be the nth previous command. If you provide a second argument, fc displays all commands from the most recent event that matches the first argument through the most recent event that matches the second. The next command displays the history list from event 197 through event 205:

```
$ fc -1 197 205
197 aspell -c letter.adams01
198 nroff letter.adams01 > adams.out
199 nroff letter.adams01 > adams.out
200 less adams.out
201 lpr adams.out
202 rm adams.out
203 cd ../
204 ls
205 rm *0486
```

The following command lists the most recent event that begins with the string view through the most recent line that begins with the letters asp:

```
$ fc -1 view asp
194 view calendar
195 cd Work
196 vi letter.adams01
197 aspell -c letter.adams01
```

To list a single command from the history file, use the same identifier for the first and second arguments. The following command lists event 197:

```
$ fc -1 197 197
197 aspell -c letter.adams01
```

# Editing and Reexecuting Previous Commands

You can use fc to edit and reexecute previous commands.

```
fc [-e editor] [first | last]]
```

When you call fc with the -e option followed by the name of an editor, fc calls the editor with event(s) in the Work Buffer. Without first and last, fc defaults to the most recent command. The next example invokes the vi editor to edit the most recent command:

```
$ fc -e vi
```