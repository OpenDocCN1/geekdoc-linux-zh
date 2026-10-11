1. The class Employee is declared.

2. The Carp module from the standard Perl library is used to handle error messages. Instead of using the built-in die function, we can use the croak method from the Carp module to exit when there is an error, with a little more detail on what caused the error.

3. The constructor method new is defined.

4. The first argument to the constructor method is the name of the class. It is shifted from the @\_ array and assigned to $class.

5. The rest of the arguments in the @\_ array are assigned to the hash %params. They were sent to the constructor as a set of key/value pairs in the @\_.

6. A reference, $ref, is assigned the address of an anonymous hash.

7. The key Name is assigned a value, retrieved from the %params hash. Error checking is done here. If a corresponding value for the key Name is not provided, the croak function will be executed, letting the user know that he did not assign a value to the Name, and the program will exit.

8. The Address property is assigned by getting its value from the %params hash.

9. This is an example of how you can make sure the user of the module passed the expected arguments. The conditional statement reads: If the %params has a key called IdNum defined, then get its value and assign it to $IdNum; otherwise, when the program runs, tell the user he forgot to include this parameter. In the examples using croak, the program will die if the user doesn’t provide input when asked for it, whereas in this form of checking, the program will continue to run.

10. After assigning properties, a reference to the object is blessed into the class and returned to the caller.

11. The instance method get\_stats is defined.

12. The first argument is shifted from the @\_ array and assigned to $self. It is a pointer to the object.

13. The foreach loop is entered. The built-in keys function extracts all the keys from the object. The keys and values are printed on the next line.

# 14.2.6 Polymorphism and Runtime Binding

Webster’s Dictionary defines polymorphism as follows:

poly·mor·phism: n. 1. the state or condition of being polymorphous.

There, that should clear things up! Here’s another definition from Webopedia.com: