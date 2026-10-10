| Operating System | Supported Compilers |
| --- | --- |
| AIX® | IBM XL C/C++ Enterprise Edition Version 7.0 for AIX<br>IBM XL C/C++ Enterprise Edition Version 8.0 for AIX<br>IBM XL C/C++ Enterprise Edition Version 9.0 for AIX |
| Linux | GNU/Linux gcc versions 3.3 and 3.4<br>Intel C Compiler Version 9.1<br>Intel C Compiler Version 10.1 |
| Windows® | Intel Proton Compiler for Windows 32-bit applications, Version 9.0.021 or later<br>Microsoft® Visual C++ .NET or later |

Table 5.1 – Supported C/C++ compilers

> Note:
> This list is not a complete list. For more details and the latest information about the supported C/C++ compiler versions, refer to the DB2 9.7 Information Center at http://publib.boulder.ibm.com/infocenter/db2luw/v9r7/topic/com.ibm.db2.luw.apdv.gs.doc/doc/r0023434.html and the DB2 Application Development Web site at: http://www.ibm.com/software/data/db2/udb/ad/

In this book we use the Microsoft Visual C++ compiler (Windows) and the GNU/Linux gcc compiler (Linux). Microsoft Visual C++ compiler is licensed software and comes with Microsoft Visual Studio. The Express version of Visual Studio can be downloaded from http://www.microsoft.com/express/Downloads/.
GNU Linux gcc compiler comes free with GNU operating systems, but can also be downloaded from http://gcc.gnu.org/.

# 5.2.2 Setting up the C/C++ environment

To set up the C/C++ environment, follow these steps:

+   1.  Verify a supported C/C++ compiler is installed
+       Make sure that a supported C/C++ compiler is installed on a DB2 Express-C supported platform. Check Table 5.1 for a list of supported compiler versions.
+       On Linux, to check whether a C/C++ compiler is installed successfully or not, issue the command below at the Linux shell:
+       `which gcc`
+       If the compiler is installed, you should get `/usr/bin/gcc` on the screen.