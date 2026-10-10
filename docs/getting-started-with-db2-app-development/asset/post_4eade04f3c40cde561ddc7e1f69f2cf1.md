
## 5.3.5 Building embedded SQL C/C++ applications

You can build an embedded SQL C/C++ application either manually from the command line or by using DB2 provided scripts. This section discusses both ways.

### 5.3.5.1 Building embedded SQL C/C++ applications from the command line

Building embedded SQL C/C++ applications from the command line involves the following steps:

- 1. Precompile the application by issuing the PRECOMPILE command
- 2. If you created a bind file (by using the BINDFILE option in the PRECOMPILE command in step 1), bind this file to a database to create an application package by issuing the BIND command.
- 3. Compile the modified application source and the source files that do not contain embedded SQL to create an application object file (a .obj file).
- 4. Link the application object files with the DB2 and host language libraries to create an executable program using the link command.

These steps are illustrated in Figure 5.14 below taken from the *developerWorks* Article *DB2 packages: Concepts, examples, and common problems*. [4]

![](img/5f6ba170efa3a607142589708531bef8_185_0.png)

Figure 5.14 – Building an embedded C/C++ SQL program

Let's take a look at each of the steps illustrated in Figure 5.14 in more detail:

#### 5.3.5.1.1 Step 1: Precompile the source file

Once you have created the embedded SQL application's source files, you must precompile each host language file containing SQL statements with the PREP command. The precompiler comments out all SQL statements contained in the source file, generates the DB2 run-time API calls for those statements and creates a BIND file when the BINDFILE option is used as shown below:

```
db2 prep embeddedC.sqc bindfile
```

Figure 5.15 shows the output of above command

![](img/5f6ba170efa3a607142589708531bef8_186_0.png)

Figure 5.15 - Precompiling a C source file using the PREP command

#### 5.3.5.1.2 Step 2: Binding the bind file

Binding is the process of creating a package on the database server out of a bind (.bnd) file that was created by the PREP command. The bind file contains the information required by DB2 such as the collection id, package name, timestamp, host variables, SQL statements, and so on, to create the package on the server. For example:

```
db2 bind embeddedC.bnd
```

Figure 5.16 provides the output of the above command.

![](img/5f6ba170efa3a607142589708531bef8_186_1.png)

Figure 5.16 - Binding a package using the BIND command

DB2 also provides a tool called db2bfd that can dump the contents of a bind file. This tool can be helpful if you want to get information about the package that it would create, without actually creating the package first.

db2bfd -b will dump header information, containing the package name, consistency token, etc. This is shown in Figure 5.17.

```
C> DB2 CLP > DB2
embeddedC.bnd: Header Contents
Header Fields:
Field Value

releaseNum 0x800
Endian 0x4c
numHosts 7
maxSent 5
numStmt 19
optInternalCnt 4
optCount 9

Name Value
Isolation Level Cursor Stability
Creator "\DBMINSTRATOR"
App Name "EMBEDDED"
Timestamp "ohrizkz-2009/18/25 19:37:43:48"
Cnulreqq Yes
Sql Error No package
Validate Bind
Date Default/local
Time Default/local
```

Figure 5.17 – Output of db2bfd -b

db2bfd -s will dump the SQL statements as shown in Figure 5.18.

```
C> DB2 CLP > DB2
C:\books\cc+>db2bfd -s embeddedC.bnd
embeddedC.bnd : SQL Statements = 19

Line Sec Typ Var Len SQL statement text
7 0 5 0 21 BEGIN DECLARE SECTION
15 0 2 0 17 END DECLARE SECTION
19 0 19 0 13 INCLUDE SQLCA
40 0 19 0 17 CONNECT TO SAMPLE
84 0 19 0 13 CONNECT RESET
109 1 0 253 INSERT INTO employee(empno, first name, lastname, edlevel, salary, VALUES <50001, 'RAUL', 'CHONG', 21, 60000>, <50
002, 'JAMES', 'JI', 29, 57862, <50003, 'HIN', 'HO', 29,
5876>, <50004, 'IAN', 'HAKES', 19, 5489>, <50005, 'UI
NET', 'MISHRA', 19, 5600>
129 0 8 0 6 COMMIT
138 2 11 1 27 PREPARE STMT FROM :H00001
156 2 9 2 39 EXECUTE STMT USING :H00006 : :H00001
170 0 8 0 6 COMMIT
188 3 15 0 123 DECLARE CURH CURSOR FOR SELECT empno, first name, lastname,
edlevel, salary FROM employee WHERE empno BETWEEN 50001
AND 50005
201 3 4 0 9 OPEN CURH
203 3 7 5 78 FETCH CURH INTO :H00001 :H00002 : :H00003 : :H00004
210 3 7 5 69 FETCH CURH INTO :H00001 :H00002 : :H00003 : :H00004
220 3 6 0 10 CLOSE CURH
221 0 8 0 6 COMMIT
251 4 0 1 37 DELETE employee WHERE empno = :H00001
264 5 0 0 51 DELETE employee WHERE empno BETWEEN 50001 AND 50005
265 0 8 0 6 COMMIT
C:\books\cc+>
```

Figure 5.18 – Output of db2bfd -s

db2bfd -v will dump the host variables as shown in Figure 5.19.

![](img/5f6ba170efa3a607142589708531bef8_188_0.png)

Figure 5.19 – Output of db2bfd -v

#### 5.3.5.1.3 Step 3: Compile the modified source file (.c) generated in Step 2

Using your C/C++ compiler, compile the _c file. For example:

```
cl -Zi -Od -c -W2 -DWIN32 embeddedC.c
```

Figure 5.20 provides the output of above command

![](img/5f6ba170efa3a607142589708531bef8_188_1.png)

Figure 5.20 – Compile the application

#### 5.3.5.1.4 Step 4: Link the file with DB2 and C libraries

Link the .obj files and the DB2 and C libraries as follows:

```
link -debug -out:embeddedC.exe embeddedC.obj db2api.lib
```

Figure 5.21 provides the output of above command.

![](img/5f6ba170efa3a607142589708531bef8_188_2.png)

Figure 5.21 – Link application with DB2 libraries

#### 5.3.5.1.5 Step 5: Execute the application

The result of step 4 is an executable file, `embeddedC`. You can run the executable file by entering the executable name (On Windows), or changing the permissions in Linux so it's an executable file (chmod +x):

```
embeddedC
```

Figure 5.22 provides the output of above command.

![](img/5f6ba170efa3a607142589708531bef8_189_0.png)

Figure 5.22 – Output of the executable file embeddedC

### 5.3.5.2 Building embedded SQL C/C++ applications using the sample build script

To build an embedded C application, the easiest way is to use `bl2app` script provided by DB2. The `bl2app` script compiles and links the embedded application. The script is located in the `sql1lib/samples/c` directory if the application is written in C. If the application is written in C++ the location of the script is `sql1lib/samples/cpp`, along with sample utility programs that can be built with these files.

`bl2app` scripts takes up to four parameters, represented inside the script file by the variables `$1`, `$2`, `$3`, and `$4`. The parameter, `$1`, specifies the name of your source file. Building embedded SQL programs requires a connection to the database so three optional parameters are also provided: the second parameter, `$2`, specifies the name of the database to which you want to connect; the third parameter, `$3`, specifies the user ID for the database, and `$4` specifies the password.

If the program contains embedded SQL, indicated by the `.sqc` extension, then the `embprep` script is called to precompile the program, producing a program file with a `.c` extension.

The following example shows how to build and run embedded C applications. To build the above sample program `embeddedC.sqc` enter:

```
bl2app embeddedC
```

Figure 5.23 provides the output, and highlights four steps which were also discussed in section 5.4.1.

![](img/5f6ba170efa3a607142589708531bef8_190_0.png)

Figure 5.23 – Output of building the application using bldapp script

The result is an executable file, embeddedC. You can run the executable file by entering the executable name:

embeddedC

## 5.5 Developing a C/C++ application with ODBC/CLI

In section 1.3.3 you were introduced to ODBC/CLI development. In this chapter we discuss this subject again, but in more detail. DB2 Call Level Interface (DB2 CLI) is IBM's callable SQL interface to the DB2 family of database servers. It is a C and C++ application programming interface for relational database access that uses function calls to pass dynamic SQL statements as function arguments. DB2 CLI is based on the Microsoft Open Database Connectivity (ODBC) specification and the International Standard for SQL/CLI. The DB2 CLI driver is included with all DB2 servers and several clients as discussed in section 1.3.3. It behaves as the ODBC driver for ODBC applications connecting to DB2.

ODBC is an alternative to embedded dynamic SQL, but unlike embedded SQL, it does not require host variables or a precompiler. The main advantage of an ODBC application over
