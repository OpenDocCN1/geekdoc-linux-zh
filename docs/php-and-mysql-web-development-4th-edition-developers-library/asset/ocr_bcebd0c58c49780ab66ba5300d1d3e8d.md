# ## 8

# # Writing MySQL Programs Using Perl DBI

T his chapter describes how to use the Perl DBI interface for MySQL. It does not discuss DBI philosophy or architecture. For information about those aspects of DBI (particularly in comparison with the C and PHP APIs), see Chapter 6, “Introduction to MySQL Programming.”

The examples discussed here draw on our sample database, sampdb, using the tables created for the grade-keeping project and for the Historical League in Chapter 1, “Getting Started with MySQL.” To get the most from this chapter, it's best if you know something about Perl. If you don't, you may be able to get along with purely your own scripts simply by copying the sample code you see here, but you will probably find a good Perl book a worthwhile investment. One such book is Programming Perl, Third Edition by Wall, Christiansen, and Orwant (O’Reilly, 2000).

DBI is currently at version 1.601, although most of the discussion here applies to earlier versions as well. DBI requires at least Perl 5.6.0 (and 5.6.1 is preferred to 5.6.0). You must also have the DBD::mysql Perl module installed, as well as the MySQL C client library and header files. If you plan to write Web-based DBI scripts in the manner discussed here, you should also obtain the CGL.pm module. In this chapter, CGL.pm is used in conjunction with the Apache Web server. If you need to obtain any of these packages, see Appendix A, “Obtaining and Installing Software.” Instructions for obtaining the example scripts developed in this chapter are also given in that appendix. They are part of the sampdb distribution, which you can download to avoid retyping the scripts yourself. The scripts used in this chapter are located under the perlapi directory of the distribution.

For the most part, this chapter describes Perl DBI methods and variables only as they are needed for the discussion here. For a more comprehensive listing of methods and variables, see Appendix H, “Perl DBI API Reference” (online). You can use that appendix as a reference for further background on any part of DBI that you're trying to use. Online documentation is available by running the following commands:

```
perldoc DBI
```