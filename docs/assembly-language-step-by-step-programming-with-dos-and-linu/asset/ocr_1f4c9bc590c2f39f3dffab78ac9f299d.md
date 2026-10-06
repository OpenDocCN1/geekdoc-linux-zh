# ASSEMBLY LANGUAGE STEP-BY-STEP

In remembering your grade-school machinations, don’t fall into the old rut of thinking, “cross out the 10, make it a 9.” In the world of hexadecimal, 10H - 1 = F. Cross out the 10, make it an F.

# What’s the Point?

... if you have a hex calculator, or a hex-capable screen calculator? The point is practice. Hexadecimal is the lingua franca of assemblers, to multiply-rangle metaphor. The more you burn a gut-level understanding of hex into your reflexes, the easier assembly language will be. Furthermore, understanding the internal structure of the machine itself will be much easier if you have that the intuitive grasp of hex values. We’re laying important groundwork here. Take it seriously now and you’ll lose hair later on.

# Binary

Hexadecimal is excellent practice for taking on the strangest number base of all: binary. Binary is base 2. Given what we’ve learned number bases so far, what can we surmise about base 2?

+   - Each column has a value two the columns to its right.
- There are only two digits (0 and 1) in the binary.

Counting is a little strange in binary, as you might imagine. It goes like this: 0, 1, 10, 11, 100, 101, 110, 111, 1000... Because it sounds absurd to say, “Zero, one, 10, 11, 100, ...” it makes more sense to enumerate the individual digits, followed by the word binary. For example, most people say “one zero one one zero zero one binary” instead of “one million, eleven thousand, one hundred and one binary” when pronouncing the number 1011101—which sounds enormous until you consider its value in decimal is only 93.

Odd as it may seem, binary follows all of the rules we’ve discussed in this chapter regarding number bases. Converting between binary and decimal is done using the same methods described for hexadecimal in an earlier section of this chapter.

Because counting in binary is as much a matter of counting columns as counting digits (since there are only two digits) it makes sense to take a long, close look at Table 2.7, which shows the values of the binary number columns out to 32 places.