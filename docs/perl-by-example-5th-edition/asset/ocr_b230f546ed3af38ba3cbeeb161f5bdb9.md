# **EXPLANATION** (_Continued_)

3  Like *Cat*, a *Dog* is a *Pet*. The only difference (in this example) between a *Dog* and a *Cat* is how they *speak*. In a real-world scenario, the differences between these classes will depend on what you are writing code to do. Perhaps your classes will contain the genomes for the particular species; perhaps just the biological classification, perhaps you want to model their behavior differently for a computer game. At any rate, attributes are inherited from the parent class.

4  As with *Cat*, the *Dog* has a *speak* method as well. If you tried to run *speak*() on an object that was not a *Cat* or a *Dog*, but just a basic *Pet*, a runtime error would occur.

5  When *speak* is called on a *Dog* object, it will say *Woof*, whereas *Cat* said *Mew*. We still use the *name*! property, which we inherited from *Pet*.

![](bbox=[0.17, 0.42, 0.57, 0.62])

**Figure C.2** The parent, subclass, and user hierarchy for the examples..

# **EXAMPLE C.12**

```
# ( ( Standard Perl script preamble used ) )
#!/usr/bin/env perl
# pet_user.pl
1 use Dog;
  use Cat;
  use warnings;
  use strict;

2 my $dog = Dog->new(
    owner  => "Daniel",
    name   => "Fido",
    gender => "M"
    );

```