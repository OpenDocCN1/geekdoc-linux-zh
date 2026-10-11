4. Rewrite the *Checking* package so it gets the balance from the file *register* if the file exists; otherwise, it will start at a zero balance. Each time the program exits, save the current balance and the time and date in the *register* file.

5. Move the *Checking* package from the *myATM* script into a file called *Checking.pm*. Now move the *Checking.pm* module into a directory called *myModules*. Update the @INC array in the *myATM* script that will use the module. Use the *Checking* module in the *myATM* script.

6. Examine the following code:

```
```Perl
package Checking;
use base qw(Exporter);
our @EXPORT_OK = qw(deposit withdraw get_balance startup onexit );
our @EXPORT_TAGS = ("transactions" =>
	[ qw(deposit withdraw get_balance startup onexit) ] );
```
```

a. How would the user import the symbols from this module?

b. Can you implement the *Exporter* module in your *Checking.pm* module?