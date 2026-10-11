# EXAMPLE 14.22 (CONTINUED)

```
3 sub count_teacher { # Class method
state $counter=0;
$counter++;
return $counter;
}
4 sub new { # Constructor for Teacher
my ($class)= shift;
my $data=@_;
my $emp = $class->init("Name"=>$data{ Name},
"StartDate"=>$data{StartDate},
"_BasePay"=>$data{_BasePay},
);
$tracker=count_teacher();
return $emp;
}
sub set_courses{
my $self=shift;
my $ctr=shift;
$self->{"_courses"}=$ctr;
}
7 sub get_courses{
my $self=shift;
return "@{$self->{ '_courses'}}";
}
8 END{
print "${tracker} teachers were created.\n";
}
```

# EXPLANATION

+   1 The Teacher class is defined here.
+   2 In this module, the @ISA is updated directly rather than by using the base.pm or parent.pm pragmas. The name of the base class is listed so that the subclass, Teacher, can inherit from it. Not only does the @ISA array need to be updated, but the use directive must name the base class and load it. This is done automatically when you say use parent or use base.
+   3 This class function will track the number of new Teacher objects added to the class.
+   4 The new() constructor method for the teacher defines the properties for the teacher as a hash and returns a blessed teacher reference.
+   5 Like the Salesman class described previously, the Teacher inherits from the Employee class and calls its init() method. The init() constructor in the Employee class will then assign the basic properties for an Employee and return a blessed Teacher object.
+   6 The teacher object is sent to the set_courses() method along with a reference to a list of courses. These courses will be set as a new attribute to the object.
+   7 The get_courses() method will retrieve and send back the list of the teacher's courses by dereferencing the pointer, $self->{_courses}.