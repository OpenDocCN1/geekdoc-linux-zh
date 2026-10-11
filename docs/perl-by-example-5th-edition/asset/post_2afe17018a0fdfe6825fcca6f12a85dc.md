
# EXERCISE 11
**I Can't Seem To Function Without Subroutines**

1. Write a program called *tripper* that will ask the user the number of miles he has driven and the amount of gas he used.
   - a. In the *tripper* script, write a subroutine called *mileage* that will calculate and return the user's mileage (miles per gallon). The number of miles driven and the amount of gas used will be passed as arguments. All variables should be *my* variables. The program should test to make sure the user doesn't enter 0 for the amount of gas. (Division by zero is illegal.)
   - b. Print the results.
   - c. Prototype *tripper*.

2. Hotels are often rated using stars to represent their score. A five-star hotel may have a king-size bed, a kitchen, and two TVs; a one-star hotel may have cockroaches and a leaky roof.
   - a. Write a subroutine called *prinstar* that will produce a histogram to show the star rating for hotels shown in the following hash. The *prinstar* function will be given two parameters: the name of the hotel and the number of its star rating. (Hint: sort the hash keys into an array. Use a loop to iterate through the keys, calling the *prinstar* function for each iteration.)

   ```perl
   %hotels=("Pillowmint Lodge"   => "5",
           "Buxton Suites"   => "5",
           "The Middletonian"   => "3",
           "Notchbelow"   => "4",
           "Rancho El Cheapo"   => "1",
           "Pile Inn"   => "2",
           );
   ```

   **OUTPUT**

   | Hotel | Category |
   | :--- | :--- |
   | Notchbelow | **** |
   | The Middletonian | *** |
   | Pillowmint Lodge | ***** |
   | Pile Inn | * |
   | Rancho El Cheapo | * |
   | Buxton Suites | ***** |

   - b. Sort the hotels by stars, five stars first, one star last. Can you sort the hash by values so that the five-star hotels are printed first, then four, and so forth? (See http://lavalinuxalexander.com/perl/edu/qanda/plqa00016.)

   | Hotel | Category |
   | :--- | :--- |
   | Buxton Suites | ***** |
   | Pillowmint Lodge | ***** |
   | Notchelow | **** |
   | The Middleton | *** |
   | Pale Inn | ** |
   | Rancho El Cheapo | * |

3. Write a grades program to take the course number and the name of a student as command-line arguments. The course numbers are CS101, CS202, and CS303. The program will include three subroutines:
   - Subroutine *ave* to calculate the overall average for a set of grades.
   - Subroutine *highest* to get the highest grade in the set.
   - Subroutine *lowest* to get the lowest grade in the set.
   - a. Print the average, the highest score, and the lowest score.
   - b. If there were any failures (average below 60), print the name, course number, and a warning to STDERR such as: Be advised: Joe Blow failed CS202.
   - c. Send the name of the failing student and the course number to a file called *failures*. Sort the file by course number.
   - d. Use the AUTOLOAD function to test that each subroutine has been defined.

4. Write a function to calculate and return the monthly payment on a loan where:

   P = principal, the initial amount of the loan  
   I = the annual interest rate (from 1 to 100 percent)  
   L = length, the length (in years) of the loan, or at least the length over which the loan is amortized

   The following assumes a typical conventional loan where the interest is compounded monthly. (See http://www.hughchou.org/calc/formula.html for tips on how to calculate mortgage loan payments.)

   - a. First, define two more variables to make the calculations easier:

   ```
   J = monthly interest in decimal form = I / (12 × 100)
   N = number of months over which loan is amortized = L × 12
   ```

   - b. Create a hash with the values of P, I, L, and pass the hash to the function. Return the monthly payment using the following formula (you must convert the formula to Perl):

   ```
   M = P * ((J / (1 - (1 + J) ^ -N))
   ```

# Chapter 12
## Does This Job Require a Reference?

![](img/8556abcb353c0991f12099420ec28735_406_0.png)

By the time you finish this chapter, you will understand the following Perl statements:

```perl
use Data::Dumper;
use warnings;
use strict;
my $student=( "Name"=>undef,
 "Major"=>undef,
 "Courses"=>[],
 "Stats"=>{},
);
$student->{"Courses"}=[ qw( French Algebra Chemistry ) ];
$student->{"Stats"}->{"PointAve"}=3.5;
$student->{"Stats"}->{"StartDate"}="09/17/12";
print Dumper $student;
```

## 12.1 What Is a Reference?

You have a post office box where you receive mail. The address on a letter contains a reference to your mailbox. The postman goes to that address and puts the letter in the box. You go to your mailbox address and pull out the letter. If you didn't have the mailbox, the postman would have to hand you the letter directly. Instead, he did it indirectly by putting it in the box. That's a simplified attempt to explain references.

A Perl reference is a variable that refers to another one. In short, it contains the address of another variable. The terms **reference** and **pointer** are often used interchangeably in Perl, because they both point to something, but they are not really the same, and those in Perl circles avoid using the term **pointer**. The main difference is that pointers in other languages contain the integer value of a memory address (for a specified data type) which you can directly manipulate. For example, with a C pointer, you can jump from element to element in an array of integers by performing pointer arithmetic, such as `p++`, where *p* contains the memory address of an array of ints. However, you can't do that with Perl references. As you know, Perl variables can hold any data type at any given time. We don't declare ints, floats, and the like. Perl handles all that. (To see how C, C++, Java, and other languages handle pointers and to get a really good introduction to pointers in general, Stanford provides a simple video called “Binky Fun With Pointers” found at http://library.stanford.edu/104/.)

Unlike pointers, Perl references are data structures that are displayed as strings, not integers. They contain the data type and the hexadecimal address of the variable they reference; for example, here is a reference to a scalar variable: `SCALAR(0x0b57c0)`. Unlike C, Perl keeps track of managing memory and of reference counts, and when there are no more references to the data, then Perl will automatically destroy the data. But, as mentioned earlier, because both references and pointers do point to something, the terms are often used interchangeably.

When you create a Perl reference, it is stored in a scalar variable. Now the big question is, “What's the point? Why do we need references?” There are three good reasons to use references:

- To pass arguments by reference to subroutines
- To create complex data structures, such as a hash of hashes, an array of arrays, a hash consisting of nested hashes, arrays, subroutines, and so forth
- To create Perl objects, as shown in the next chapter

Perl has two types of references: hard references and symbolic references. The hard references were introduced with Perl 5. Before hard references, typglob aliases were used, but were of limited usefulness, other than for manipulating the internal symbol table (see Section 13.1.4, “The Symbol Table,” in Chapter 13, “Modularize It, Package It, and Send It to the Library”). A symbolic reference is when a variable holds the name of another variable and is also of limited use (http://perlmaven.com/symbolic-reference-in-perl). Although this chapter focuses on hard references, we will include a discussion of symbolic references and typglobs at the end of the chapter.

### 12.1.1 Hard References

A *hard reference* is a scalar that holds the address of another variable or subroutine. It is an indirect way to access a variable. Perl references not only contain the hexadecimal address, but the data type:

```
ARRAY (0x7f9241004e08)
```

The reference can point to (reference) a scalar, an array, a hash, a subroutine, a typglob, another reference, and so forth.
