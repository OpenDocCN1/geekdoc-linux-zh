# **Analytic number theory.** There are many important results in number theory that can be established by using methods from analysis. For example, analytic methods developed by G. F. B. Riemann in 1859 were used by J. Hadamard and C. J. de la Vallée Poussin in 1896 to prove the famous prime number theorem. This theorem, first conjectured by Gauss around 1793, states that *r*(*x*), the number of primes not exceeding *x*, behaves as shown in Eq. (4). These methods of Riemann are based on ζ(*s*), the function defined by Eq. (5), where *s* = *σ* + *it* is a complex variable; the series in this equation is convergent for *σ* > 1. Via an analytic continuation, this function can be defined in the whole complex plane. It is a meromorphic function with only a simple pole of residue 1 at *s* = 1. It can be shown that ζ(*s*) has no zeros for *σ* = 1; this result and the existence of a pole at *s* = 1 suffice to prove the prime number theorem. Riemann’s work contains the still unproved so-called Riemann hypothesis: all zeros of ζ(*s*) have a real part not exceeding 1/2. See COMPLEX NUMBERS AND COMPLEX VARIABLES.

```
$$ \lim_{x \to \infty} \frac{\pi(x)}{(x/\log x)} = 1 $$
```

```
$$ \zeta(s) = \sum_{n=1}^{\infty} \frac{1}{n^s} $$
```

# **Diophantine approximation.** A real number *x* is called *rational* if there are integers *p* and *q* such that *x* = *p/q*; otherwise *x* is called *irrational*. The number $b^{1/m}$ is irrational if *b* is an integer which is not the *m*th power of an integer (for example, 2 is irrational). A real number *x* is called *algebraic* if it is the root of a monic polynomial with integer coefficients; otherwise *x* is called *transcendental*. The numbers *e* and *π* are transcendental. That *π* is transcendental implies that it is impossible to square the circle. See CIRCLE, *E* (MATHEMATICS).

The part of number theory called diophantine approximation is devoted to approximating numbers of a particular kind by numbers from a particular set, such as approximating irrational numbers by rational numbers with small denominators. A basic result is that, given an irrational number *r*, there exist infinitely many fractions *h/k* that satisfy the inequality (6), where *k* is any positive number not exceeding 5. However, where *c* is greater than 5, there are irrational numbers *r* for which there are only finitely many such *h/k*.

```
$$ \left| x - \frac{h}{k} \right| < \frac{1}{c k^2} $$
```

In 1851, J. Liouville showed that transcendental numbers exist; he did so by demonstrating that the number *x* given by Eq. (7) has the property that, given any positive real number *m*, there is a rational number *h/k* that satisfies Eq. (8). See ALGEBRA; NUMBERING SYSTEMS; ZERO. [K.H.R.]

```
$$ x = \sum_{j=1}^{\infty} 10^{-j!} $$
```

```
$$ \left| x - \frac{h}{k} \right| < \frac{1}{k^m} $$
```

# **Numbering systems** A numbering system is a systematic method for representing numbers using a particular set of symbols. The most commonly used numbering system is the decimal system, based on the number 10, which is called the *basis* or *radix* of the system. The basis tells how many different individual symbols there are in the system to represent numbers. In the decimal system these symbols are the digits 0, 1, 2, 3, 4, 5, 6, 7, 8, 9. The range of these symbols varies from 0 to (10 − 1). This is a particular case of a more general rule: Given any positive basis or radix *N*, there are *N* different individual symbols that can be used to write numbers in that system. The range of these numbers varies from 0 to *N* − 1.

In the computer and telecommunication fields, three of the most frequently used numbering systems are the binary (base 2), the octal (base 8), and the hexadecimal (base 16). The binary system can have only two symbols: 0 and 1. Either of these symbols can be called a binary *digit* or a *bit*. The octal system has eight symbols: 0, 1, 2, 3, 4, 5, 6, 7. The hexadecimal system has 16 symbols: 0, 1, 2, 3, 4, 5, 6, 7, 8, 9, A, B, C, D, E, F. A stands for 10, B for 11, C for 12, D for 13, E for 14, and F for 15. The reason for choosing single letters to represent numbers higher than 9 is to keep all individual symbols single characters. See BIT.

All the numbering systems mentioned so far are *positional systems*. That is, the value of any symbol depends on its position in the number. For example, the value of 2 in the decimal number 132 is that of two units. In the decimal system, the rightmost position of a number is called the *ones* (10$^0$) place, the next position from the right is called the *tens* (10$^1$) place, the next position the *hundreds* (10$^2$) place, and so on. Observe that the powers increase from the right. The power of the rightmost digit is zero, the power of the next digit is one, the power of the next digit is two, and so on. These powers are sometimes called the *weight* of the digit. **Conversion to decimal numbers.** In any positional system the decimal equivalent of a digit in the representation of the number is the digit’s own value, in decimal, multiplied by a power of the basis in which the number is represented. The sum of all these powers is the decimal equivalent of the number. The corresponding powers of each of the digits can be better visualized by writing superscripts beginning with 0 at the rightmost digit, and increasing the powers by 1 in moving toward the left digits of the number.

**Decimal numbers to other bases.** The conversion of a given decimal number to another basis *r* (>0) is carried out by initially dividing the given decimal number by *r*, and then successively dividing the resulting quotients by *r* until a zero quotient is obtained. The decimal equivalent is obtained by writing the remainders of the successive divisions in the opposite order in which they were obtained.

**Binary to hexadecimal or octal and vice versa.** The table shows the decimal numbers 1 through 15 written in binary, octal, and hexadecimal. Since each four-bit binary number corresponds to one and only one hexadecimal digit and vice versa, the hexadecimal system can be viewed as a shorthand notation of the binary system. Similar reasoning can be applied to the octal system. This one-to-one correspondence between the symbols of the binary system and the symbols of the octal and hexadecimal system provides a method for converting numbers between these bases.

To convert binary numbers to hexadecimal, the following procedure may be used: (1) Form four-bit groups beginning from the rightmost bit of the number. If the last group (at the leftmost part of the number) has fewer than 4 bits, add leading zeros.

| Binary | Octal | Hexadecimal | Decimal |
| :--- | :--- | :--- | :--- |
| 0001 | 1 | 1 | 1 |
| 0010 | 2 | 2 | 2 |
| 0011 | 3 | 3 | 3 |
| 0100 | 4 | 4 | 4 |
| 0101 | 5 | 5 | 5 |
| 0110 | 6 | 6 | 6 |
| 0111 | 7 | 7 | 7 |
| 1000 | 10 | 8 | 8 |
| 1001 | 11 | 9 | 9 |
| 1010 | 12 | A | 10 |
| 1011 | 13 | B | 11 |
| 1100 | 14 | C | 12 |
| 1101 | 15 | D | 13 |
| 1110 | 16 | E | 14 |
| 1111 | 17 | F | 15 |

(2) Replace each group of four bits with its hexadecimal equivalent from the table.