
# Glossary

This glossary defines terms and abbreviations used in this publication. If you do not find the term you are looking for, refer to the index portion of this book. This glossary includes terms and definitions from:

- *IBM Dictionary of Computing*, New York: McGraw Hill (1-800-2MC-GRAW), 1994.
- *American National Standard Dictionary for Information Systems*, ANSI X3.172-1990, copyright 1990 by the American National Standards Institute (ANSI). Copies may be purchased from the American National Standards Institute, 11 West 42nd Street, New York, New York 10036. Definitions are identified by the symbol (A) after the definition.
- *Information Technology Vocabulary*, developed by Subcommittee 1, Joint Technical Committee 1, of the International Organization for Standardization and the International Electrotechnical Commission (ISO/IEC JTC1/SC1). Definitions from published sections of these vocabularies are identified by the symbol (I) after the definition. Definitions taken from draft international standards, committee drafts, and working papers being developed by ISO/IEC JTC1/SC1 are identified by the symbol (T) after the definition, indicating that final agreement has not yet been reached among the participating National Bodies of SC1.

**APAR.** Authorized Program Analysis Report. A report of a problem caused by a suspected defect in a current unreleased release of a program.

**argument.** A parameter passed between a calling program and a SUBROUTINE subprogram, a FUNCTION subprogram, or a statement function.

**array.** An ordered set of data items identified by a single name.

**array element.** A data item in an array, identified by the array name followed by a subscript indicating its position in the array.

**array name.** The name of an ordered set of data items that make up an array.

**assignment statement.** A statement that assigns a value to a variable or array element. It is made up of a variable or array element, followed by an equal sign ( = ), followed by an expression. The variable, array element, or expression can be character, logical, or arithmetic. When the assignment statement is processed, the expression to the right of the equal sign replaces the value of the variable or array element to the left.

**Basic Linear Algebra Subprograms (BLAS).** A standard, public domain, set of mathematical subroutines that perform linear algebra operations.

**BLAS.** Basic Linear Algebra Subprograms.

**cache.** A special-purpose buffer storage, smaller and faster than main storage, used to hold a copy of instructions and data obtained from main storage and likely to be needed next by the processor. (T)

**character constant.** A string of one or more alphanumeric characters enclosed in apostrophes. The delimiting apostrophes are not part of the value of the constant.

**character expression.** An expression in the form of a single character constant, variable, array element, substring, function reference, or another expression enclosed in parentheses. A character expression is always of type character.

**character type.** The data type for representing strings of alphanumeric characters; in storage, one byte is used for each character.

**column-major order.** A sequencing method used for storing multidimensional arrays according to the subscripts of the array elements. In this method the leftmost subscript position varies most rapidly and completes a full cycle before the next subscript position to the right is incremented.

**complex conjugate even data.** Complex data that has its real part even and its imaginary part odd.

**complex constant.** An ordered pair of real or integer constants separated by a comma and enclosed in parentheses. The first real constant of the pair is the real part of the complex number; the second is the imaginary part.

**complex type.** The data type for representing an approximation of the value of a complex number. A data item of this type consists of an ordered pair of real data items separated by a comma and enclosed in parentheses. The first item represents the real part of the complex number; the second represents the imaginary part.

**constant.** An unvarying quantity. The four classes of constants specify numbers (arithmetic), truth values (logical), character data (character), and hexadecimal data.

**data type.** The structural characteristics, features and properties of data that may be directly specified by a programming language; for example, integers, real numbers in Fortran; arrays in APL; linked lists in LISP; character string in SNOBOL.

**decoration.** The formation of a sequence containing every *n*-th element of another sequence.

**dimension of an array.** One of the subscript expression positions in a subscript for an array. In Fortran, an array may have from one to seven dimensions. Graphically, the first dimension is represented by the rows, the second by the columns, and the third by the planes. Contrast with rank. See also extent of a dimension.

**direct access storage.** A storage device in which the access time is in effect independent of the location of the data. (A)

**divide-by-zero exception.** The condition recognized by a processor that results from running a program that attempts to divide by zero.

**double precision.** Synonym for long-precision.

**expression.** A notation that represents a value: a primary appearing alone, or combinations of primaries and operators. An expression can be arithmetic, character, logical, or relational.

**extent of a dimension.** The number of different integer values that may be represented by subscript expressions for a particular dimension in a subscript for an array.

**external function.** A function defined outside the program unit that refers to it. It may be referred to in a procedure subprogram or in the main program, but it must not refer to itself, either directly or indirectly. Contrast with statement function.

**function.** In Fortran, a procedure that is invoked by referring to it in an expression and that supplies a value to the expression. The value supplied is the value of the function. See also external function, intrinsic function, and statement function. Contrast with subroutine.

**function reference.** A Fortran source program reference to an intrinsic function, to an external function, or to a statement function.

**general matrix.** A matrix with no assumed special properties such as symmetry. Synonym for matrix.

**integer constant.** A string of decimal digits containing no decimal point and expressing a whole number.

**integer expression.** An arithmetic expression whose values are of integer type.

**integer type.** An arithmetic data type capable of expressing the value of an integer. It can have a positive, negative, or 0 value. It must not include a decimal point.

**intrinsic function.** A function, supplied by Fortran, that performs mathematical or character operations.

**leading dimension.** For a two-dimensional array, an increment used to find the starting point for the matrix elements in each successive column of the array.

**logical constant.** A constant that can have one of two values: true or false. The form of these values in Fortran is: .TRUE. and .FALSE., respectively.

**logical expression.** A logical primary alone or a combination of logical primaries and logical operators. A logical expression can have one of two values: true or false.

**logical type.** The data type for data items that can have the value true or false and upon which logical operations such as .NOT. and .OR. can be performed. See also “data type”.

**long-precision.** Real type of data of length 8. Contrast with single precision and short-precision.

**main program.** In Fortran, a program unit, required for running, that can call other program units but cannot be called by them.

**mask.** To use a pattern of characters to control the retention or elimination of portions of another pattern of characters. (I)

**matrix.** A rectangular array of elements, arranged in rows and columns, that may be manipulated according to the rules of matrix algebra. (A) (I)

**multithreaded.** There may be one or more threads in a process, and each thread is executed by the operating system concurrently. An application program is multithreaded if more than one thread is executed concurrently.

**overflow exception.** A condition caused by the result of an arithmetic operation having a magnitude that exceeds the largest possible number.

**platform.** A mainframe or a workstation.

**primary.** An irreducible unit of data; a single constant, variable, array element, function reference, or expression enclosed in parentheses.
