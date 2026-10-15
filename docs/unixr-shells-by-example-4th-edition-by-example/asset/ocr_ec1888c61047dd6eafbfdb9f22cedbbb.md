Lab 60: Loops 964
Lab 61: Functions 965

# 15 Debugging Shell Scripts 967

+   15.1 Introduction 967
+   15.2 Style Issues 967
+   15.3 Types of Errors 968
+       15.3.1 Runtime Errors 969
+       15.3.2 Naming Conventions 969
+       15.3.3 Insufficient Permissions 970
+       15.3.4 Path Problems 970
+       15.3.5 The Shbang Line 972
+       15.3.6 Sneaky Aliases 973
+   15.4 Probable Causes for Syntax Errors 975
+       15.4.1 Undefined and Misspelled Variables 975
+       15.4.2 Incomplete Programming Statements 976
+           Missing Keywords 976
+           Indentation 976
+           if/endif Errors 977
+           case and switch Errors 978
+           Looping Errors 979
+           Operator Errors 981
+           Misusing an Operator 982
+           Quoting Errors 983
+           Quoting Metacharacters 983
+           What You Should Know About Quotes 985
+           Problems with the here document 989
+           File-Testing Errors 990
+       15.4.3 Common Error Messages from the Big 5 Shells 991
+           Common C/TC Shell Error Messages 992
+           Common Bourne Shell Error Messages 994
+           Common Korn Shell Error Messages 996
+           Common Bash Error Messages 999
+       15.4.4 Logic Errors and Robustness 1001
+           Logical Operator Errors 1001
+           Relational Operator Errors 1002
+           Branching Errors 1003
+           Exit Status with an if Conditional 1004
+           Lacking Robustness 1005
+   15.5 Tracing with Shell Options and the set Command 1009
+       15.5.1 Debugging Bourne Shell Scripts 1009
+           Bourne Shell Debugging Options 1009
+       15.5.2 Debugging C/TC Shell Scripts 1011
+       15.5.3 Debugging Korn Shell Scripts 1014