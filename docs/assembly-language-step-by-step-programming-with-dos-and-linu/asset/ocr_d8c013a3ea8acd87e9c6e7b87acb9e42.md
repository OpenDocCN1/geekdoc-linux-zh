# ASSEMBLY LANGUAGE BY-STEP

```
38E3:0150 44 C7 06 28 8B 1C 44 C7E-F6 26 8D 01 8C 29 46 .V..&...&.......F
38E3:0160 F2 89 56 54 2B C9 51 06-57 FF 76 0A F7 76 0E .V..+Q.W...V....
38E3:0170 88 83 06 50 FF 76 06 04 9A 4B 05 EF 32 FF .P..P.V..W...K.2.
```

Sam, as you care, is now something else entirely.

Now, something went a little bit wrong when you Changed Sam a man to a moose. Look closely at memory starting at address 0111H. After the "e" (65H) is half of an EOL marker. The carriage return character (0DH) is gone, because you wrote an "e" over it. The line feed character (0AH) remains.

This isn't fatal, it isn't right. A lonely line feed in a text file can cause trouble or not, depending on what you try to do with it. If you load the altered SAM.TXT into the NASM-IDE text editor (I explain NASM-IDE in Chapter 5), you'll see a peculiar symbol with a circle in the middle of it after the word "moose." This is how the NASM-IDE editor indicates certain invisible characters that are not EOL or EOF markers, by using the graphical symbol set from the PC character ROM. The rectangle-with-circle tells you that a nonprintable character is present at that point in the file. (Load the CD-ROM file MOOSE.TXT into NASM-IDE and you'll see what I mean.)

The lesson here is that DEBUG is a loaded gun without a safety catch. There are no safeguards. You can change anything inside a file with it, whether it makes sense or not, or whether it's dangerous or not. All safety considerations are up to you. You must be aware of whether or not you're overwriting important parts of the file.

This is a theme that will occur again and again in assembly language: Safety is up to you. Unlike Basic, which wraps a protective cocoon around you and keeps you from banging yourself up too badly, assembly language lets you hang yourself without a whimper of protest.
Keep this in mind as we continue.

# Examining and Changing Registers

If you saved SAM.TXT back out to disk in its altered state, you created a damaged file. (I did this for you, by creating the file MOOSE.TXT.) Fixing SAM.TXT requires reconstructing the last EOL marker by inserting the CR character that you wrote using the E Command. Unfortunately, this means you'll be making SAM.TXT larger than it was when DEBUG read it into memory. To save the corrected file back out to disk,