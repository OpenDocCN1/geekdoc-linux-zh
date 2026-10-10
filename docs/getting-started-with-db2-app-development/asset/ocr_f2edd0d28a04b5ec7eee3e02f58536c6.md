# ### 9.5 Summary

In this chapter, you have learned how to set up a Perl environment to work with DB2, and how to execute SQL statements and call stored procedures from Perl applications by calling the standard Perl DBI interface.

# ### 9.6 Review questions

+   1. Which API can a Perl application use to access a DB2 database?

+   2. What's the relationship between the Perl DBI and the database DBD drivers?

+   3. Which of the following is the standard database interface for a Perl script to access a DB2 database?
+      A. CLI
+      B. Embedded Perl
+      C. Perl DBI
+      D. JDBC
+      E. None of the above

+   4. Which of the following are the steps you can use to execute a SQL with parameter marker?
+      A. prepare, bind_param, execute
+      B. prepare, bind_variable, do
+      C. prepare, bind_param, do
+      D. prepare, do, fetchrow_array
+      E. None of the above

+   5. Which of the following functions can be used to execute a SQL directly without first preparing it?
+      A. exec_immediate
+      B. execute
+      C. do
+      D. execute_imm
+      E. None of the above