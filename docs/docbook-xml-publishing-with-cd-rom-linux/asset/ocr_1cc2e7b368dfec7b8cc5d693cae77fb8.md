# Chapter 12: Creating Technical Documents

This section will cover using DocBook markup to describe actions performed at the command line.

# Commands and Options

The next example will probably look fairly familiar. It's a short paragraph describing how to use SGMLTools to create HTML output from a file called filename.sgml.

```
<!DOCTYPE article PUBLIC "//OASIS//DTD DocBook V4.1//EN">
<article>
<title>Using SGMLTools</title>
<para>To render HTML from a DocBook file, if you use the following syntax.</para>
<para><prompt>user@host:~\$</prompt><command>sgmltools</command> <option>-b html=</option> <filename>filename.sgml</filename></para>
</article>
```

The Prompt element is used to indicate a command prompt, in this case a standard Linux prompt, but it can be used to indicate a DOS prompt or any other type of prompt as well. The Command element is used to indicate any program or executable name that you would type at the command line.

The Filename attribute is used to indicate any filename, including the name of a directory. Figure 12.8 shows the output from the example in HTML. Note the command name and options.

If you want to demonstrate the use of a command with optional arguments, you use the Optional element. For instance, if you want to demonstrate the use of the UNIX ls command with an optional argument like the color argument, then you would use a syntax like the next example. Figure 12.9 shows what this example looks like rendered in HTML.

```
<! article PUBLIC "//OASIS//DTD DocBook V4.1//EN">
<article>
<title>Using ls to list directories in Color</title>
<para>To display the contents of a directory use the <command>ls</command> command. To see the display in color, you can use the color argument.</para>
<para><prompt>user@host:~\$</prompt><command>ls</command> <optional>-color</optional></para>
</article>
```