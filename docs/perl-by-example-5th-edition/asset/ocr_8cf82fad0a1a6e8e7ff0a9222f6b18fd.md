the mere mention of them. You can assign strings, numbers, or a combination of these to Perl variables and Perl will figure out what the type is. You may store a number or a list of numbers in a variable and then later change your mind and store a string there. Perl doesn't care.

A scalar variable contains a single value (for example, one string or one number), an array variable contains an ordered list of values indexed by a positive number, and a hash contains an unordered set of key/value pairs indexed by a string (the key) that is associated with a corresponding value (see Figure 5.1). (See Section 5.2, "Scalars, Arrays, and Hashes.")

### package main
| scalar namespace | array namespace | hash namespace |
| :--- | :--- | :--- |
| \$friend | @course<br>\$course[0] | %department<br>\$department{Ed} |

**Figure 5.1** Namespaces for scalars, arrays, and hashes in package main.

# ### 5.1.2 Package, Scope, Privacy, and Strictness

**Package and Scope.** The Perl sample programs you have seen in the previous chapters are compiled internally into what is called a **package**, which provides a **namespace** for variables.

An analogy often used to describe a package is the naming of a person. In the Johnson family, there is a boy named James. James is known to his family and does not have to qualify his name with a last name every time he is being called to dinner. "James, sit down at the table" is enough. However, in the school he attends there are several boys named James. The correct James is identified by his last name, for example, "James Johnson," or to the principal's office."

In a Perl program, "James" represents a variable and his family name, "Johnson," a package. The default package is called main. If you create a variable, *Sname*, for example, *Sname* belongs to the main package and could be identified as *$main:name*, but qualifying the variable at this point is unnecessary as long as we are working in a single file and using the default package, main. Later when working with modules, we will step outside of the package main. This would be like James going to school. Then we could have a conflict if two variables from different packages had the same name and would have to qualify which package they belong to. For now, we will stay in the main package. When you see the word main in a warning or error message, just be aware that it is a reference to something going on in your main package.

The scope of a variable determines where it is visible in the program. In the Perl scripts you have seen so far, the variables live in the package main and are visible to the entire script file (that is, global in scope). Global variables, also called package variables, can be