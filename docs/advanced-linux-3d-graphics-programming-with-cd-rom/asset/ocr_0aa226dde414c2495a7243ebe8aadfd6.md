Method ``dif`` takes a second vertex as a parameter, and returns the vector difference between the location of the current vertex and the location of the second vertex—in other words, the vector from the second vertex to the current vertex.

```
Listing 6-1: Vertex.pm
package Vertex;
use strict;

# the object constructor #
sub new {
    my $proto = shift;
    my $class = ref($proto) || $proto;
    my $self = {};
    $self->{x} = undef;
    $self->{y} = undef;
    $self->{z} = undef;
    bless ($self, $class);
    return $self;
}

## methods to access per-object data #
## With args, they set the value. Without ##
## any, they only retrieve it/them. #####
sub x {
    my $self = shift;
    if (0_) {$self->{x} = shift }
    return $self->{x};
}

sub y {
    my $self = shift;
    if (0_) {$self->{y} = shift }
    return $self->{y};
}

sub z {
    my $self = shift;
    if (0_) {$self->{z} = shift }
    return $self->{z};
}

sub dot {
    my $self = shift;
    my $v2 = shift;
    return $self->{x} * $v2->x +
           $self->{y} * $v2->y +
           $self->{z} * $v2->z ;
}
```