
## Contents

- F.6 mysql.server ............................ 1070
- F.6.1 Options Supported by mysql.server ............................ 1070
- F.7 mysql_config ............................ 1071
- F.7.1 Options Specific to mysql_config ............................ 1071
- F.8 mysql_install_db ............................ 1071
- F.8.1 Standard Options Supported by mysql_install_db ............................ 1072
- F.8.2 Options Specific to mysql_install_db ............................ 1072
- F.9 mysqladmin ............................ 1072
- F.9.1 Standard Options Supported by mysqladmin ............................ 1073
- F.9.2 Options Specific to mysqladmin ............................ 1073
- F.9.3 Variables for mysqladmin ............................ 1074
- F.9.4 mysqladmin Commands ............................ 1074
- F.10 mysqlbinlog ............................ 1076
- F.10.1 Standard Options Supported by mysqlbinlog ............................ 1076
- F.10.2 Options Specific to mysqlbinlog ............................ 1077
- F.10.3 Variables for mysqlbinlog ............................ 1079
- F.11 mysqlcheck ............................ 1079
- F.11.1 Standard Options Supported by mysqlcheck ............................ 1079
- F.11.2 Options Specific to mysqlcheck ............................ 1080
- F.12 mysqld ............................ 1083
- F.12.1 Standard Options Supported by mysqld ............................ 1083
- F.12.2 Options Specific to mysqld ............................ 1084
- F.12.3 Variables for mysqld ............................ 1100
- F.13 mysqld_multi ............................ 1101
- F.13.1 Standard Options Supported by mysqld_multi ............................ 1101
- F.13.2 Options Specific to mysqld_multi ............................ 1101
- F.14 mysqld_safe ............................ 1102
- F.14.1 Standard Options Supported by mysqld_safe ............................ 1102
- F.14.2 Options Specific to mysqld_safe ............................ 1102
- F.15 mysqldump ............................ 1104
- F.15.1 Standard Options Supported by mysqldump ............................ 1105
- F.15.2 Options Specific to mysqldump ............................ 1105
- F.15.3 Data Format Options for mysqldump ............................ 1112
- F.15.4 Variables for mysqldump ............................ 1112
- F.16 mysqlhotcopy ............................ 1113
- F.16.1 Standard Options Supported by mysqlhotcopy ............................ 1114
- F.16.2 Options Specific to mysqlhotcopy ............................ 1114
- F.17 mysqlimport ............................................................. 1116
- F.17.1 Standard Options Supported by *mysqlimport* ........ 1117
- F.17.2 Options Specific to *mysqlimport* ...................... 1117
- F.17.3 Data Format Options for *mysqlimport* ................. 1118
- F.18 mysqlshow ............................................................ 1119
- F.18.1 Standard Options Supported by *mysqlshow* .......... 1119
- F.18.2 Options Specific to *mysqlshow* ...................... 1119
- F.19 perror ................................................................. 1120
- F.19.1 Standard Options Supported by *perror* ................. 1120

> Note: Appendixes G, H, and I are located online and are accessible either by registering this book at Informit.com/register or by visiting www.kitebird.com/mysql-book.

- G C API Reference ..................................................... 1121
- G.1 Compiling and Linking ....................................... 1122
- G.2 C API Data Types .............................................. 1123
- G.2.1 Scalar Data Types ....................................... 1123
- G.2.2 Non-Scalar Data Types ................................... 1124
- G.2.3 Accessor Macros .......................................... 1135
- G.3 C API Functions .................................................. 1136
- G.3.1 Client Library Initialization and Termination Routines .. 1136
- G.3.2 Connection Management Routines ........................ 1137
- G.3.3 Error-Reporting Routines .................................. 1149
- G.3.4 Statement Construction and Execution Routines .......... 1150
- G.3.5 Result Set Processing Routines ............................ 1152
- G.3.6 Information Routines ..................................... 1161
- G.3.7 Transaction Control Routines ............................ 1164
- G.3.8 Multiple Result Set Routines ............................ 1164
- G.3.9 Prepared Statement Routines ........................... 1165
- G.3.10 Administrative Routines ................................ 1173
- G.3.11 Threaded Client Routines ................................. 1175
- G.3.12 Debugging Routines ...................................... 1175
- H Perl DBI API Reference ............................................... 1177
- H.1 Writing Scripts ................................................... 1178
- H.2 DBI Methods ...................................................... 1178
- H.2.1 DBI Class Methods .................................... 1180
- H.2.2 Database-Handle Methods ................................ 1185
- H.2.3 Statement-Handle Methods . . . . . . . . . . . . . . . . . . 1191
- H.2.4 General Handle Methods . . . . . . . . . . . . . . . . . . . 1195
- H.2.5 MySQL-Specific Administrative Methods . . . . . . . . . . . . . 1196
- H.3 DBI Utility Functions . . . . . . . . . . . . . . . . . . . . . . . 1197
- H.4 DBI Attributes . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 1198
- H.4.1 Database-Handle Attributes . . . . . . . . . . . . . . . . . . 1198
- H.4.2 General Handle Attributes . . . . . . . . . . . . . . . . . . 1199
- H.4.3 MySQL-Specific Database-Handle Attributes . . . . . . . . . . 1200
- H.4.4 Statement-Handle Attributes . . . . . . . . . . . . . . . . . . 1201
- H.4.5 MySQL-Specific Statement-Handle Attributes . . . . . . . . . 1203
- H.4.6 Dynamic Attributes . . . . . . . . . . . . . . . . . . . . . . . 1205
- H.5 DBI Environment Variables . . . . . . . . . . . . . . . . . . . . 1205
- **I PHP API Reference** . . . . . . . . . . . . . . . . . . . . . . . . . . 1207
- I.1 Writing PHP Scripts . . . . . . . . . . . . . . . . . . . . . . . . . 1207
- I.2 PDO Classes . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 1208
- I.3 PDO Methods . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 1208
- I.3.1 PDO Class Methods . . . . . . . . . . . . . . . . . . . . . . . . 1209
- I.3.2 PDOStatement Object Methods . . . . . . . . . . . . . . . . . 1215
- I.3.3 PDOException Object Methods . . . . . . . . . . . . . . . . . 1222
- I.3.4 PDO Constants . . . . . . . . . . . . . . . . . . . . . . . . . . 1223
- **Index** . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 1225

## About the Author

Paul DuBois is a writer, database administrator, and leader in the open source and MySQL communities. He has contributed to the online documentation for MySQL and is the author of *MySQL and Perl for the Web* (New Riders), *MySQL Cookbook*, *Using ssh and rsh*, and *Software Portability with make* (O’Reilly). He is currently a technical writer with the MySQL documentation team at Sun Microsystems.

## Acknowledgments

Acknowledgments are presented here by edition.

### Fourth Edition

My technical reviewers, Stephen Frein and Tim Boronczyk, identified many points that needed correction or clarification. Ulf Wendel and Johannes Schlüter made comments and corrections on the PHP material. My thanks to each of them.

The staff at Pearson responsible for this edition were Mark Tابر, Acquisitions Editor; Michael Thurston, Development Editor; Jovana San Nicolas-Shirley, Project Editor; Jake McFarland, Compositor; Cheryl Lenser, Indexer; and Gary Adair, Cover Designer.

To my wife Karen, my continued thanks and gratitude for her encouragement and support throughout this effort.

### Third Edition

The third edition enjoyed careful technical review by Zak Grent and Chris Newman. Their efforts improved the manuscript at many points. Monty and the developers at MySQL AB also provided insight in response to my questions.

The people at Pearson responsible for this edition were Shelley Johnston, Acquisitions Editor; Damon Jordan, Development Editor; and Andy Beaster, Project Editor.

I am happy to recognize that my wife Karen again deserves special credit for her support during yet more revision and rewriting.

### Second Edition

For the second edition, the technical reviewers once again played a crucial role in finding errors and making corrections and clarifications. Hang Lau and Shane Kirk served as reviewers. I’d also like to thank Monty Widenius, Alexander Barkov, Jani Tolonen, and the other MySQL developers for patiently enduring my many questions and supplying answers that made their way into these pages.

The New Riders staff that brought this edition to life were Stephanie Wall, Associate Publisher; Chris Zahn, Development Editor; Lori Lyons, Senior Project Editor; Pat Kinyon, Copy Editor; Cheryl Lenser, Indexer; and Stacey Richwine-DeRome, Compositor.

And, as always, my wife Karen provided the behind-the-scenes support that readers do not see, but without which this book would be much poorer.
