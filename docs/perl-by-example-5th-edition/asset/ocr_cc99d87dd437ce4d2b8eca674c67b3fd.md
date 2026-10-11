# EXPLANATION

+   1. The *Employee.pm* module will be used by this program.
+   2. *warnings* will be issued for possible errors, and the *strict* pragma will track global and undefined variables, barewords, and so forth.
+   3. A list of lexical private variables is created.
+   4. The user of the program will be asked for the information that will be passed to the *Employee* module.
+   5. The constructor is called to pass arguments as key/value pairs; that is, a hash is passed to the constructor in the *Employee* module. A reference to the object is returned and assigned to $Employee.
+   6. The instance method *get_stats* is called to display the employee's attributes.

In the next example, let's see how the module handles its named parameters.

# EXAMPLE 14.8

```
# Module Employee.pm—See Example 14.7 to use this module.
package Employee;
use Carp;
sub new {
  my $class = shift;
  my ($param) = @_; # Receiving the hash that was passed
  my $ref = {
    "Name" => $params{"Name"} || croak("No name assigned"),
    "Extension" => $params{"Extension"},
    "Address" => $params{"Address"},
    "PayCheck" => $params{"PayCheck"} || croak("No pay assigned"),
    ((defined $params{"_IdNum"}) ? ("_IdNum" => $params{"_IdNum"}) : croak("Employee's id was not provided!\n"))
  };
  return bless($ref, $class);
}
sub get_stats {
  my $self = shift;
  foreach my $key (keys %params, %$self) {
    print $key, " ", $self->{$key}, "\n";
  }
  print "\n";
}
```