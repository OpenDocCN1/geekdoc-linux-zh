# SYNTAX

```
uuencode [option] [source-file] decode_label
uuencode [-o output-file] [source-file] decode_label
```

Purpose: Convert source file from binary to ASCII
Output: First syntax: the encoded version of source-file to standard output
Second syntax: the encoded version of source-file to output-file

# Commonly used options/features:

+   -m Use Base64 method of encoding instead of the standard algorithm

```
uudecode [options] [encoded-file]
```

Purpose: Decode encoded-file from ASCII to binary
Output: The binary version of encoded-file into a file called decode-label, the second parameter of the uuencode command

# Commonly used options/features:

+   -i Do not overwrite files
+   -p Send the decoded (binary) version of the file to standard output
+   -o output_file Send the decoded (binary) version of the file to output_file

The uuencode command sends the encoded (ASCII) version of the file to standard output. The command takes input from standard input if no source-file is specified in the command. The output has decode_label in the header (first line) of the ASCII version.

The uudecode utility recreates the original file from the uuencoded (ASCII) file and puts it in a file called decode_label. With the -p option, the command sends the binary version to standard output. This option uses the uudecode command in a pipeline (see Chapter 9). Both the uuencode and uudecode commands retain the original files that they translate. The diagram shown in Figure 7.1 illustrates the process of uuencoding and uudecoding.

You can redirect the output to a file by using the > symbol, as shown in the uuencode a.out alarm.out > sarwar.out command in the following session. When you do so, the encoded output goes to the file sarwar.out with a decode_label of alarm.out.

```
% cat a.out
ELF >'@@?
@@@@@@@@@@@@ ' '( '??000P?@$$Q?T/libexec/ld-elf.
so.FreeBSD>FreeBSD
```

![](bbox=[0.15, 0.00135, 0.88, 0.00155])

FIGURE 7.1 The process of uuencoding and uudecoding.