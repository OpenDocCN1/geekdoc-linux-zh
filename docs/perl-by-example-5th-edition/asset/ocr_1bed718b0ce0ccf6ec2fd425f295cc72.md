# C.3 The Attributes

6 `'show_student'` is called to show that the course has been removed from the array.

7 The `get_courses` method was defined by the handles option in the `courses'` attribute. The student's courses are printed. The list contains *linear_algebra* but not *topology*.

8 We have created two new students. The *student_count* accessor is called and returns 2.

9 A new block is created and a lexical variable declared. It will go out of scope when the block ends. It is assigned a new *Student* object, with data. The *DEMOLISH* method will be called and destroy the variable when it goes out of scope; meaning, when the block ends. See *Demolish* in the output.

10 The *student_count* is now 3.

11 Outside the block, the object, `$student3`, has gone out of scope and is destroyed. Now when we inspect that class attribute again, it is back to 2.

# C.3.5 Example Using Inheritance with Moose

We talked about Perl OO and inheritance in Chapter 14, “Bless Those Things! (Object- Oriented Perl).” Also in Chapter 14, we discussed Moose roles (see Section 14.4.4, “Multiple Inheritance and Roles with Moose”.)

The following Moose examples consist of four files: a parent (*Pet.pm*), two sub classes (*Dog.pm* and *Cat.pm*), and a user (*petuser.pl*). The purpose of these examples is to give you a brief introduction to how Moose simplifies inheritance.

![](bbox=[0.08, 0.545, 0.48, 0.72])

**Figure C.1** The parent and subclass hierarchy for the following examples.

```
```
 (The Parent Class)
 # Pet.pm
 1 package Pet;
 2 use Moose;
 3 has 'owner' => (
         is => 'str',
         rw => 'rw'
     );
```
```