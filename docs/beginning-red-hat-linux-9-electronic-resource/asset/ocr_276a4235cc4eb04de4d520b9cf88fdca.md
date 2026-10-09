You can save this application in `send_email.pl` and proceed to run it, like so:

```
```perl
$ perl send_email.pl
syntax error at send_email.pl line 15, near ")"

print"
Global symbol "$email" requires explicit package name at send_email.pl line 23.
Global symbol "$email" requires explicit package name at send_email.pl line 24.
Global symbol "$email" requires explicit package name at send_email.pl line 26.
Global symbol "$email" requires explicit package name at send_email.pl line 28.
Global symbol "$email" requires explicit package name at send_email.pl line 58.
Global symbol "$email" requires explicit package name at send_email.pl line 78.
Execution of send_email.pl aborted due to compilation errors.
```
```

Perl is telling us there are errors in our code. The first error is at or around line 15. And the second set of errors claim that we are using the `$email` variable without pre-declaring it first. Take a look at the code. You should see that we purposely left out the semicolon at the end of line 12 and declared a variable called `$emale` instead of `$email`. The line numbers that Perl reports in the errors may not always be exact, due to the manner in which it parses the code, so you should check the entire area around the reported error for any possible bugs.

# ## Fixing Errors and Checking Syntax

If you are getting other errors, you may have forgotten to install the `Mail::Send` module properly, as shown in the *Installing Extensions* section earlier in the chapter. It is also possible that you may have made a mistake in typing the code. Why don't you fix the broken code in the application, adding the necessary semicolon and correcting the misspelled variable:

```
```perl
my ($email, $answer, $subject, $message);
```
```

Let's run it again, but before we do so, we will check its syntax and structure. We can use Perl's `-w` and `-c` options, which report warnings and check syntax, respectively, to check the status of our code, like so:

```
```bash
$ perl -wc send_email.pl
send_email syntax OK
```
```

If there are no problems with the code, Perl returns the output shown above. You should make it a point to check the syntax of your applications in this manner before running them, so that you can catch possible errors quickly. We are now ready to go through the code, after which we will look at how to actually use this application, including a screenshot of a sample session.