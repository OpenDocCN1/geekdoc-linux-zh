# EXAMPLE 2.2 (CONTINUED)

```
```
# Dereference pointer
print ${$ref1};    # Dereference pointer to scalar; prints: 25
print ${$ref2};    # Dereference pointer to array;
                   # prints: Nick Cht Susan Dolly
print ${$ref3};    # Dereference pointer to hash;
                   # prints: styleSaltboxpicenegetablewoonerBank of America
print ${$ref2}->[1];
print ${$ref3}->{"style"};    # prints "Saltbox"
print @{$arrayref};    # prints elements of unnamed array
print %{$hashref};    # prints elements of unnamed hash
```
```

**Objects.** Perl supports objects, a special type of reference. A Perl class is a package containing a collection of variables and functions, called properties and methods. There is no *class* keyword. The properties (also called *attributes*) describe the object. Methods are special functions that allow you to create and manipulate the object. Objects are created with the *bless* function (see Chapter 14, “Bless Those Things! (Object-Oriented Perl)”).

# Creating a Class

# EXAMPLE 2.3

```
```
package Pet;

sub new{  # Constructor
my $class = shift;
my $pet = {
"Name" => undef,
"Owner" => undef,
"Type" => undef,
};
return bless($pet, $class);  # Returns a reference to the object
}

sub set_pet{ # Accessor methods
my $self = shift;
my ($name, $owner, $type) = @_;
$self->{'Name'} = $name;
$self->{'Owner'} = $owner;
$self->{'Type'} = $type;
}

sub display_pet{
my $self = shift;
while(($Key,$Value)=each(${$self})){
print "$Key: $Value\n";
}
}
```
;
```