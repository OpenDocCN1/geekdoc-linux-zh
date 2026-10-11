# ## 15.6 Transactions

| | EXPLANATION |
|---|:---|
| **1** | Constants representing the values of the SQL standard types are included with the special DBI::sql\_Types tag. The constants are used by the bind\_param method starting on line 10. |
| **2** | Connection to the MySQL database is made. |
| **3** | The RaiseError attribute is turned on to catch exceptions and die if there is one. |
| **4** | The AutoCommit attribute is turned off, so that SQL statements are not automatically sent to the database, but must be manually committed. |
| **5** | A list of anonymous arrays is created to represent the rows that will be inserted into the table. |
| **6** | A SQL statement is created to insert new teams later; the values to be substituted for the ? placeholders. |
| **7** | The SQL statement is prepared. A statement handle is returned. |
| **8** | The foreach loop is used to iterate through each of the rows that will be added. |
| **9** | The eval block is entered. If an error occurred, it will be assigned to the special variable, $@. See line 11. |
| **10** | The bind\_param() method binds the first parameter to the first (?) placeholder in line 6. The first parameter, Param->\[0\] is 'Tampa Terrors', the first time in the loop. It is of type SQL\_VARCHAR. Next, the second parameter, param->\[1\] is bound to the second placeholder (?), the first time through the loop, it represents the number of wins, which is 3. |
| **11** | If we got this far, we will commit. |
| **12** | If the statement fails, eval sets the $@ special variable to the error that occured and will issue a warning that this transaction will be rolled back and will not be committed. |
| **13** | If the statement failed, it is rolled back. |

# ### 15.6.2  Perl DBI, the Web, and the Dancer Framework

Back in the old days, starting in 1993, CGI (Common Gateway Interface) was used to create dynamic Web pages. Writing these pages required configuring the HTTP server (normally Apache), dealing with HTTP headers, requests/responses, as well as environment variables, producing HTML code, understanding HTTP error messages, and more. In the previous edition of this book, a great deal of time was spent explaining how to write these scripts which not only required a considerable understanding of Perl, but also of HTML and HTTP.

When CGI.pm was added to the standard Perl library, it provided a solution to simplify writing CGI scripts and handling HTTP requests/responses by adding features for creating forms, file uploads, cookies, and other utilities. However, CGI.pm is not simple; its big and clunky, and to be effective requires a fairly advanced understanding of how the CGI protocol works, not to mention knowing Perl and HTML in depth. The problem was that more often the designer didn't know Perl and the programmer didn't know how to design.