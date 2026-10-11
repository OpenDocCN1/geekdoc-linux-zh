# EXAMPLE 14.3 (CONTINUED)

```
```
# Create the instance methods that will manipulate the object
# The setter methods
3 sub set_owner{    # Access or instance methods
4     my ($self, $owner) = @_;
# First argument is a pointer to the house object
5     $self->{"Owner"}=$owner;    # Set a new owner
}
sub set_color{    # Setter method
    my ($self,$color) = @_;
# First argument is a pointer to the house object.
    $self->{"Color"}=$color;
}
sub set_payment{
    my ($self, $payment) = @_;
# First argument is a pointer to the house object
    $self->{"Payment"}=$payment;
}
# The getter methods
6 sub get_owner{
7     my $self=shift;
        return $self->{"Owner"};
}
sub get_color{
    my $self=shift;
        return $self->{"Color"};
}
sub get_payment{
    my $self=shift;
        return $self->{"Payment"};
}
```
```

# EXPLANATION

+   1. The class is House.
+   2. The constructor is defined with default properties.
+   3. The instance methods are defined here. This is the set_owner method, called a “setter” (mutator). It stores the data in the object.
+   4. The first argument received by the set_owner method is a reference to the object. It is called $self. $self is commonly used, but the method can be called any valid variable name. The second argument is the value of the Owner property for the object. When the method is called by the user, Perl implicitly sends a reference to the object first and then any other arguments sent by the user.
+   5. A reference to the object is stored in $self. The value of the Owner property is assigned to the object via this reference.
+   6. This method is called a “getter.” It retrieves (gets) information from the object. The first argument is the address of the object, $self.
+   7. The value of the Owner property is retrieved and returned to the user.