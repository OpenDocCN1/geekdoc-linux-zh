# cat

```
`cat filename`
```

Although the `cat` command has optional arguments, they are not typically used in scripts, so we won't discuss them here. In scripts, `cat` is typically used to output a file's contents, most often for use in a pipe sequence.

For example, the command `cat /etc/issue` produces the following output:

```
```
Red Hat Linux release 7.3 (Valhalla)
Kernel 2.4.18-3 on an i686
```
```

# cut

```
`cut [options] filename(s)`
```

The `cut` command is often used in scripts or in a piped command, to cut specific fields or characters from a file in a delimited format. The default delimiter is a tab, but you can change this with the `--d` option, so that the fields in a comma or pipe-delimited file may be cut out, too.

Consider a file in this format:

```
```
12	34	54	23	12	34
32	67	85	18	62	10
```
```

The command to output fields 1 and 5 from each line of a tab-delimited file looks like this:

```
```
cut --f1,5 filename
12	12
32	62
```
```

Now let's assume a pipe-delimited file in the following format, perhaps listing the names of system administrators responsible for backing up the system on each of the seven days of the week.

```
```
john|mary|terri|leonard|jacob|geoffrey|eric
tom|jeff|mike|larry|moe|curly|harpo
```
```

To cut out the name of the person responsible for the fourth day of weeks 1 and 2, you'd use this command:

```
```
cut -d"|" -f4 filename
leonard
larry
```
```

The `cut` command has several options to provide for actions besides cutting by whole fields. You can cut specific bytes, characters, or fields. You've seen that fields are specified by the `-f` parameter. To designate the retrieval of bytes, use `-b`; and for characters, use `-c`. To indicate the inclusion of all data between the *nth* byte, field, or character and the end of the line, add a hyphen character (`-`) after the number, as shown in the following examples:

```
```
cut -d"|" -f4- filename
leonard|jacob|geoffrey|eric
larry|moe|curly|harpo
```
```