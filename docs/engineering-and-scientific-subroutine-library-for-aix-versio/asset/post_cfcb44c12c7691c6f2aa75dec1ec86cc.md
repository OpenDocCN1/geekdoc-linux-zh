
## program exception.

The condition recognized by a processor that results from running a program that improperly specifies or uses instructions, operands, or control information.

## PTF.

Program Temporary Fix. A temporary solution or by-pass of a problem diagnosed by IBM as resulting from a defect in a current unaltered release of the program. A report of a problem caused by a suspected defect in a current unaltered release of a program.

## pthread.

A thread that conforms to the POSIX Threads Programming Model.

## real constant.

A string of decimal digits that expresses a real number. A real constant must contain either a decimal point or a decimal exponent and may contain both. For example, the real constant 0.36819E+2 has the value +36.819.

## real type.

An arithmetic data type, capable of approximating the value of a real number. It can have a positive, negative, or 0 value.

## row-major order.

A sequencing method used for storing multidimensional arrays according to the subscripts of the array elements. In this method the rightmost subscript position varies most rapidly and completes a full cycle before the next subscript position to the left is incremented.

## scalar.

(1) A quantity characterized by a single number.
(2) Contrast with vector.

## shape of an array.

The extents of all the dimensions of an array listed in order. For example, the shape of a three-dimensional array that has four rows, five columns, and three planes is (4,5,3) or 4 by 5 by 3.

## short-precision.

Real type data of length 4. Contrast with double precision and long-precision.

## single precision.

Synonym for short-precision.

## size of an array.

The number of elements in an array. This is the product of the extents of its dimensions.

## SMP.

Symmetric Multi-Processing.

## statement.

(1) The basic unit of a program, that specifies an action to be performed, or the nature and characteristics of the data to be processed, or information about the program itself. Statements fall into two broad classes: executable and nonexecutable.

## statement function.

A procedure specified by a single statement that is similar in form to an arithmetic, logical, or character assignment statement. The statement must appear after the specification statements and before the first executable statement. In the remainder of the program it can be referenced as a function. A statement function may be referred to only in the program unit in which it is defined. Contrast with external function.

## statement label.

A number of from one through five decimal digits that is used to identify a statement. Statement labels can be used to transfer control, to define the range of a DO, or to refer to a FORMAT statement.

## statement number.

See “statement label”.

## stride.

The increment used to step through array storage to select the vector or matrix elements from the array.

## subprogram.

A program unit that is invoked by another program unit in the same program. In Fortran, a subprogram has a FUNCTION, SUBROUTINE, or BLOCK DATA statement as its first statement.

## subscript.

(1) A symbol that is associated with the name of a set to identify a particular subset or element.
(2) A subscript expression or set of subscript expressions, enclosed in parentheses and used with an array name to identify a particular array element.

## subscript expression.

An integer expression in a subscript whose value and position in the subscript determine the index number for the corresponding dimension in the referenced array.

## thread.

A thread is the element that is scheduled, and to which resources such as execution time, locks, and queues may be assigned. There may be one or more threads in a process, and each thread is executed by the operating system concurrently.

## thread-safe.

A subroutine which may be called from multiple threads of the same process simultaneously.

## type declaration.

The explicit specification of the type of a constant, variable, array, or function by use of an explicit type specification statement.

## underflow exception.

A condition caused by the result of an arithmetic operation having a magnitude less than the smallest possible nonzero number.

## variable.

(1) A quantity that can assume any of a given set of values.
(2) A data item, identified by a name, that is not a named constant, array, or array element, and that can assume different values at different times during program processing.

## vector.

A one-dimensional ordered collection of numbers.

## working storage.

A storage area provided by the application program for the use of an ESL subroutine.

## workstation.

A workstation is a single-user, high-performance microcomputer (or even a minicomputer) which has been specialized in some way, usually for graphics output. Such a machine has a screen and a keyboard, but is also capable of extensive processing of your input before it is passed to the host. Likewise, the host's responses may be extensively processed before being passed along to your screen. A workstation may be intelligent enough to do much or all the processing itself.

# Bibliography

This bibliography lists the publications that you may need to use with ESSL and describes how to obtain them.

# References

Text books and articles covering the mathematical aspects of ESSL are listed in this section, as well as several software libraries available from other companies. They are listed alphabetically as follows:

- Publications are listed by the author’s name. *IBM* publications that include an order number, other than an *IBM Technical Report* can be ordered through the Subscription Library Services System (SLSS). The non-IBM publications listed here should be obtained through publishers, bookstores, or professional computing organizations.
- Software libraries are listed by their product name. Each reference includes the names, addresses, and phone numbers of the companies from which they can be obtained.

Each citation in the text of this book is shown as a number enclosed in square brackets. It indicates the number of the item listed in the bibliography. For example, reference [1] cites the first item listed below.

1. Agarwal, R. C. Dec. 1984. “An Efficient Formulation of the Mixed-Radix FFT Algorithm.” *Proceedings of the International Conference on Computers, Systems, and Signal Processing*, 769–772. Bangalore, India.
2. Agarwal, R. C. August 1988. “A Vector and Parallel Implementation of the FFT Algorithm on the IBM 3090.” *Proceedings from the IFIP WG 2.5 (International Federation for Information Processing Working Conference 5)*, Stanford University.
3. Agarwal, R. C. 1989. “A Vector and Parallel Implementation of the FFT Algorithm on the IBM 3090.” *Aspects of Computation on Asynchronous Parallel Processors*, 45–54. Edited by M. H. Wright. Elsevier Science Publishers, New York, N. Y.
4. Agarwal, R. C.; Cooley, J. W. March 1986. “Fourier Transform and Convolution Subroutines for the IBM 3090 Vector Facility.” *IBM Journal of Research and Development*, 30(2):145–162 (Order no. G322-0146).
5. Agarwal, R. C.; Cooley, J. W. September 1987. “Vectorized Mixed-Radix Discrete Fourier Transform Algorithms” *IEEE Proceedings*, 75:1283–1292.
6. Agarwal, R.; Cooley, J.; Gustavson F.; Shearer J.; Shishman G.; Tuckerman B. March 1986. “New Scalar and Vector Elementary Functions for the IBM System /370.” *IBM Journal of Research and Development*, 30(2):126–144 (Order no. G322-0146).
7. Agarwal, R.; Gustavson F.; Zubair, M. May 1994. “An Efficient Parallel Algorithm for the 3-D FFT NAS Parallel Benchmark.” *Proceedings of IEEE SHPPCC 94*:129–133.
8. Andersson, E.; Bai, Z.; Bishof, C.; Demmel, J.; Dongarra, J.; DuCroz, J.; Greenbaum, A.; Hammarling, S.; McKenney, A.; Ostrouchov, S.; Sorensen, D. 1995. LAPACK: *A Portable Linear Algebra Library for High-Performance Computers* LAPACK User’s Guide (second edition), SIAM Publications, Philadelphia, Pa.
   For more information, see:
   http://www.netlib.org/lapack/index.html
