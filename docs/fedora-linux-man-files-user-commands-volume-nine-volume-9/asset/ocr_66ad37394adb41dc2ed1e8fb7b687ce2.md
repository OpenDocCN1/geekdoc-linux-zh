# OPTIONS

-b basena

Specifies the base filena for the .rsa and .sf files in the META-INF directory to conform with the JAR format. For example, `-b signatures` causes the files to be nad signatures.rsa and signatures.sf. The default is signtool.

-c#

Specifies the compression level for the -J or -Z option. The syol # represents a nuer from 0 to 9, where 0 ans no compression and 9 ans maxim compression. The higher the level of compression, the smaller the output but the longer the operation takes. If the -c# option is not used with either the -J or the -Z options, the default compression value used by both the -J and -Z options is 6.

-d certdir

Specifies your certificate database directory; that is, the directory in which you placed your key3.db and cert7.db files. To specify the current directory, use “-d.” (including the period). The Unix version of signtool assus ~/.netscape unless told otherwise. The NT version of signtool always requires the use of the -d option to specify where the database files are located.

-e extension

Tells signtool to sign only files with the given extension; for example, use `-e“.class”` to sign only Java class files. Note that with Netscape Signing Tool version 1.1 and later this option can appear multiple tis on one command line, making it possible to specify multiple file types or classes to include.

-f commandfile

Specifies a text file containing Netscape Signing Tool options and arugnts in keyword=value format. All options and arugnts can be expressed through this file. For more information about the syntax used with this file, see “Tips and Techniques”.

-G nickna

Generates a new private-public key pair and corresponding object-signing certificate with the given nickna. The newly generated keys and certificate are installed into the key and certificate databases in the directory specified by the -d option. With the NT version of Netscape Signing Tool, you st use the -d option with the -G option. With the Unix version of Netscape Signing Tool, omitting the -d option causes the tool to install the keys and certificate in the Communicator key and certificate databases. If you are installing the keys and certificate in the Communicator databases, you st exit