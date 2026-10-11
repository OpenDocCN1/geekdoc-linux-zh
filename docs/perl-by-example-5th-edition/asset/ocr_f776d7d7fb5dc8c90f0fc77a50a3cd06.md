Example E.2 shows the contents of lib/Example.pm. This is the file that contains the actual behavior of the application. app.pl is just a helper script that launches it. The welcome page, pictured, is simply the contents of views/index.tt. Templates and views are explained later in this appendix.

# EXAMPLE E.2

```
```
1 package Example;
2 use Dancer ':syntax';

3 our $VERSION = '0.1';

4 get '/' => sub {
5     template 'index';
   };

6 true;
```
```

# EXPLANATION

+   1.  This is a normal Perl module found in Example.pm, and it contains the Example package. Dancer ensures that the lib directory is available in `@INC`. app.pl uses Dancer and then uses this module. This module then tells Dancer how to behave. It is possible to have app.pl directly tell Dancer how to behave, but then we haven't written reusable or testable code. The Example module could be used by a Dancer test suite, and instead of launching the Web server, it could run automated tests that ensure whatever Example does is consistent and correct.

+   2.  This module needs Dancer syntax, but not all the rest of Dancer behavior. The use line uses syntax familiar from Exporter (see Chapter 13, "Modularize It, Package It, and Send It to the Library!") to import the syntax group. The Dancer docs list exactly what this contains.

+   3.  This is version 0.1 of our Web application—the very first version! This number will normally go up as our application is released, and this information will be useful if we put our application as a distribution on CPAN.

+   4.  This is the first part of the real body of the application. Dancer is told that, when a get request arrives to // (the root of the Web site), the subroutine should be run. This is a reference to an anonymous subroutine.

+   5.  Dancer is told to render the template called index.

+   6.  Dancer exports some constants that we can use to make our code more legible. You may prefer to use 1, like in other modules, because not all modules use Dancer, and so true is not always available.