```
$ cat > sample.txt
This text is being entered at the keyboard and
cat is copying it to a file.
Press CONTROL-D to indicate the
end of file.
CONTROL-D
$
```

**Figure 7-7** cat with its output redirected

larger file. The first three commands display the contents of three files: stationery, tape, and pens. The next command shows cat with three filenames as arguments. When you call it with more than one filename, cat copies the files, one at a time, to standard output. This command redirects standard output to the file supply_orders. The final cat command shows that supply_orders contains the contents of all three of the original files.

# # REDIRECTING STANDARD INPUT

Just as you can redirect standard output, so you can redirect standard input. The redirect input symbol (< instructs you to redirect a command's input from the specified file instead of the keyboard (Figure 7-9, next page). The format of a command line that redirects input is

```
command [arguments] < filename
```

where command is any executable program (such as an application program or a utility), arguments are optional arguments, and filename is the name of the ordinary file she redirects the input from.

| $ stationery |
| 2,000 sheets letterhead ordered: 10/7/10 |
| $ tape |
| 1 box masking tape ordered: 10/14/10 |
| 5 boxes filament tape ordered: 10/28/10 |
| $ pens |
| 12 doz. black pens ordered: 10/4/10 |

| $ stationery tape pens > supply_orders |
| $ supply_orders |
| 2,000 sheets letterhead ordered: 10/7/10 |
| 1 box masking tape ordered: 10/14/10 |
| 5 boxes filament tape ordered: 10/28/10 |
| 12 doz. black pens ordered: 10/4/10 |
| $ |

**Figure 7-8** Using cat to catenate files