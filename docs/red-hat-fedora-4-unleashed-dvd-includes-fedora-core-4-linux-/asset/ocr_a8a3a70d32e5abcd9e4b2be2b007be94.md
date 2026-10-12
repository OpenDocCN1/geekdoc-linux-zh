# ## An Example of Conversions in Action

Crafting complex conversion entries is a task perhaps best left to the Linux/Unix expert, but the sample ftpconversions file included with wu-ftpd provides more than enough examples for the average Red Hat administrator. Building your own simple conversion entry is not really too difficult, so let's examine and decode an example:

```
::Z:: /bin/compress -d -c %s:T_REG|T_ASCII:0:UNCOMPRESS:UNCOMPRESS
```

In this example, the strip prefix (field 1) is null because it is not yet implemented, so this rule does not apply to prefixes. The second field of this rule contains the .Z postfix; thus it deals with files that have been compressed with the compress utility. The rule does not address the add-on prefix or postfix, so fields 3 and 4 are null. Field 5, the external command field, tells the server to run the compress utility to decompress all files that have the .Z extension, as the -d parameter signifies. The -c options tells compress to write the output of the compress utility to the standard out, which is the server in this case. The %s is the name of the file that the rule was applied against. Field 6 specifies that this file is a regular file in ASCII format. Field 7, the options field, tells the server that this command uncompresses the file. Finally, the last field is a comment that gives the administrator a quick decode of what the conversion rule is doing, that is, uncompressing the file.

> Several conversion rules may be specified in wu-ftpd's default ftpconversions file. Additional examples, such as for Sun's Solaris operating system, might also be available in additional wu-ftpd documentation.

# ## Using Commands in the ftphosts File to Allow or Deny FTP Server Connection

The purpose of the ftphosts file is to allow or deny specific users or addresses from connecting to the FTP server. The format of the file is the word allow or deny optionally followed by a username, followed by an IP or a DNS address.

+   allow username address  
+   deny username address

Listing 22.4 shows a sample configuration of this file.

```
# Example host access file  
#  
# Everything after a '#' is treated as comment,  
# empty lines are ignored  
allow tdc 128.0.0.1
```

```
# Example host access file  
#  
# Everything after a '#' is treated as comment,  
# empty lines are ignored  
allow tdc 128.0.0.1
```

```
# Example host access file  
#  
# Everything after a '#' is treated as comment,  
# empty lines are ignored  
allow tdc 128.0.0.1
```