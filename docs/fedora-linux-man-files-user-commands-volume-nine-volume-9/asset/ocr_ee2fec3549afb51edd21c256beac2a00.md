# ## DESCRIPTION

**soelim** reads *files* and replaces lines of the form

```
.so~file
```

by the contents of *file*. It is useful if files included with `.so` need to be preprocessed. Normally, **soelim** should be invoked with the `-s` option of **groff**.

To eed “” in the file na, write ‘\’ or ‘\e’. To eed a space, write “”. Any other escape sequence in *file* makes **soelim** ignore the whole line.

Note that there st be no whitespace between the leading dot and the two characters ‘s’ and ‘o’. Otherwise, only **groff** interprets the `.so` request (and **soelim** ignores it).