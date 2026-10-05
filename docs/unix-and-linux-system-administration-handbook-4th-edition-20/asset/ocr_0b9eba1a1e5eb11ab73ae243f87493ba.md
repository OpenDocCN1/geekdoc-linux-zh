# Accepting and validating input

The traditional C-style for loop is also available:

```
for ($counter=1; $counter <= 10; $counter++) {
    printf("$counter");
}
```

We've shown you with the traditional for and foreach labels, but those are in fact
tame keyword in Perl and you can use whichever form you prefer.

Versions of Perl 5.10 (2007) have no explicit case or switch statement, but
there are several ways to accomplish the same thing. In addition to the obvious-
but-clunky option of cascading if statements, another possibility is to use a for
statement to set the value of $_ and provide a context from which last can escape:

```
for (@ARGV[]) {
    m/^webview/ && do print("Install for webserver\n"; last);
    m/tomcat/ && do print("Install for tomcat\n"; last);
    m/geronimo/ && do print("Install for geronimo\n"; last);

    print("Invalid option supplied\n"; 1);
}
```

The regular expressions are compared with the argument stored in $_ Unsuccess-
ful matches short-circuit the && and fall through to the next test. Once a
regex matches, the corresponding do block is executed. The last statements escape
from the block immediately.

# Accepting and validating input

The script below combines many of the Perl constructs we reviewed over the
last few pages, including a subroutine, postfix if statements, and a for loop.
The program itself is merely a wrapper around the main function get_string,
generic input validation routine. This routine prompts for a string, removes any
tailing newline, and verifies that the string is not null. Null strings cause the
prom to be repeated up to three times, after the script gives up.

```
#/usr/bin/perl

$maxatt = 3; # Maximum tries to supply valid input
```

```
sub get_string {
    my ($prompt, $response) = shift;
    # Try to read input up to $maxatt < $maxatt; $maxatt++) {
        print("Please try again.\n" if $maxatt;
        print("prompt: ");
        $response = readline("STDIN");
        chomp($response);
        return $response if $response;
    }
    die("Too many failed input attempts\n\n}
```

![](bbox=[0.953, 0.142, 0.991, 0.249])