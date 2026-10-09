![](bbox=[0.43, 0.09, 0.75, 0.28])

Figure 5-5  Redirecting standard input

The next example shows how to run `cat` and use the redirect output symbol to *catenate* (join one after the other—the derivation of the name of the *cat* utility) several files into one larger file. The first three commands display the contents of three files: *stationery*, *tape*, and *pens*. The next command shows `cat` with three filenames as arguments. When you call it with more than one filename, *cat* copies the files, one at a time, to standard output. This command redirects standard output to the file named *supply_orders*. The final `cat` command shows that *supply_orders* contains the contents of the three original files.

```
```text
$ cat stationery
2,000 sheets letterhead ordered:      October 7
$ cat tape
1 box masking tape ordered:           October 14
5 boxes filament tape ordered:        October 28
$ cat pens
12 doz. black pens ordered:           October 4
```
```

```
```text
$ cat stationery tape pens > supply_orders
```
```

```
```text
$ cat supply_orders
2,000 sheets letterhead ordered:      October 7
1 box masking tape ordered:           October 14
5 boxes filament tape ordered:        October 28
12 doz. black pens ordered:           October 4
```
```

# **UDD** REDIRECTING STANDARD INPUT

Just as you can redirect standard output, so you can redirect standard input. The *redirect input symbol* (`<`) instructs the shell to redirect a command's input to come from the specified file instead of from the keyboard (Figure 5-5). The syntax of a command line that redirects input is

```
```text
command [arguments] < filename
```
```

where *command* is any executable program (such as an application program or a utility), *arguments* are optional arguments, and *filename* is the name of the ordinary file the shell redirects the input from.