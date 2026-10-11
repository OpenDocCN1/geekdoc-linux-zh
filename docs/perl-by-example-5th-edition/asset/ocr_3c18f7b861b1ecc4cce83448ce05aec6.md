# **EXAMPLE 15-41 (CONTINUED)**

```
19          `<? FOREACH coach IN rows ?>`
20              `<tr>`
21                  `<? FOREACH field IN coach ?>`
22                      `<td><? field ?></td>`
23                  `<? END ?>`
24              `</tr>`
25          `<? END ?>`
        `</table>`
`</body>`
`</html>`
```

# **EXPLANATION**

+   1. The standard *shebang* is used. This ensures that if *perlbrew* is in use, the local Perl is used, instead of the system one. (See Appendix D, "Perlbrew, CPAN, and cpanm," for more information on *perlbrew*.)
+   2. The script will use *strict* to catch obvious mistakes such as misspelled variable names.
+   3. The script will use *warnings* to catch less obvious mistakes, such as undefined values being used.
+   4. The script runs under Perl 5.16 or later.
+   5. This is a Dancer script. For an introduction to Dancer, see Appendix E, "Dancing with Perl."
+   6. This is also a DBI script. Dancer can actually be configured to connect to DBI, but we're going to show a manual connection in this script. The *DBI* and *DBD::mysql* modules will be needed. See Appendix D for details on using *cpanm* to install these, if necessary.
+   7. Dancer is configured here. This can also be done in the *config.yml* shown in the Appendix E. This particular Dancer script does not require any of the extra files created in Appendix E; it runs independently.
+   8.  When the root path '/' is requested, this codefrag will run.
+       Perl will read from the DATA filehandle, found at the bottom of this script, and assign what is read to single variable, *$html*. The *do() construct simply creates a small block as a single expression, returns the result of the last statement, and assigns the result to *$html*, a *state* variable. (The *state* keyword is like *my*, except if the sub runs again, the previous value is kept, allowing the page to be refreshed without setting and reading from DATA again.) A special Perl variable, *$/*, is the input record separator with the newline being its default; meaning, each line in a file is terminated by the newline character. If set to *undef*, then all the data will be read as a single line and stored in *$html*.
+       9.  DBI is given the DSN to connect to the MySQL database running on *localhost*, with the username *root* and the password *quigley*. The database *sample_db* is selected as well. The database may also be selected after connection.