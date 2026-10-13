combine the signature with a given file or generate one separately. To combine a signature with a file, you generate a new version that incorporates both. Use the --sign or -s option to generate a version of the document that includes the digital signature. In the following example, the mydoc file is digitally signed with mydoc.gpg file containing both the original file and the signature.

```
gpg -o mydoc.gpg --sign mydoc
```

If, instead, you want to just generate a separate signature file, you use the --detach-sig command. This has the advantage of not having to generate a complete copy of the original file. That file remains untouched. The signature file usually has an extension like .sig. In the following example, the user creates a signature file called mydoc2.sig for the mydoc2 file.

```
gpg -o mydoc2.sig --detach-sig mydoc2
```

To verify the file using a detached signature, the recipient user specifies both the signature file and the original file.

```
gpg --verify mydoc2.sig mydoc2
```

You could also generate a clear sign signature to be used in text files. A clear sign signature is a text version of the signature that can be attached to a text file. The text file can be further edited by any text editor. Use the --clearsign option to create a clear sign signature. The following example creates a clear signed version of a text file called mynotice.txt.

```
gpg -o mysignnotice.txt --clearsign mynotice.txt
```