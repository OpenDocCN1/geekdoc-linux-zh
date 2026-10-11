+   5.2 Creating and Removing Directories ............................ 130

+   5.3 Reading Directories ................................................ 132

+   5.3.1 Basic Directory Reading ............................................ 133

+   5.3.1.1 Portability Considerations .................................... 136

+   5.3.1.2 Linux and BSD Directory Entries ................................ 137

+   5.3.2 BSD Directory Positioning Functions ............................... 138

+   5.4 Obtaining Information about Files ................................... 139

+   5.4.1 Linux File Types ................................................................ 139

+   5.4.2 Retrieving File Information ....................................... 141

+   5.4.3 Linux Only: Specifying Higher-Precision File Times .............. 143

+   5.4.4 Determining File Type ............................................. 144

+   5.4.4.1 Device Information ............................................... 147

+   5.4.4.2 The V7 cat Revisited .............................................. 150

+   5.4.5 Working with Symbolic Links ..................................... 151

+   5.5 Changing Ownership, Permission, and Modification Times .......... 155

+   5.5.1 Changing File Ownership: chown( ), fchown( ), and lchown( ) ... 155

+   5.5.2 Changing Permissions: chmod( ) and fchmod( ) ...................... 156

+   5.5.3 Changing Timestamps: time() ....................................... 157

+   5.5.3.1 Faking utime( file , NULL ) ..................................... 159

+   5.5.4 Using fchown( ) and fchmod( ) for Security ....................... 161

+   5.6 Summary ...................................................................... 162

+   Exercises ....................................................................... 163

+   Chapter 6 General Library Interfaces — Part 1 .......................... 165

+   6.1 Times and Dates ........................................................... 166

+   6.1.1 Retrieving the Current Time: time( ) and difftime( ) ............ 167

+   6.1.2 Breaking Down Times: gmtime( ) and localtime( ) .............. 168

+   6.1.3 Formatting Dates and Times .......................................... 170

+   6.1.3.1 Simple Time Formatting: asctime( ) and ctime( ) ........ 170

+   6.1.3.2 Complex Time Formatting: strftime( ) ....................... 171

+   6.1.4 Converting a Broken-Down Time to a time_t ........................ 176

+   6.1.5 Getting Time-Zone Information ..................................... 178

+   6.1.5.1 BSD Systems Gotcha: timezone( ), Not time_zone ........ 179

+   6.2 Sorting and Searching Functions .................................... 181

+   6.2.1 Sorting: qsort( ) ...................................................... 181