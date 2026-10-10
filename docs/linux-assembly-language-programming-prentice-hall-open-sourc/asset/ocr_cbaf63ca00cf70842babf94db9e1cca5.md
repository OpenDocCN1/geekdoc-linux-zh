eight-bit processor, or whatever.

The contents of a four-bit register are very naturally specified using a four-digit binary number. The four-digit binary numbers are the integers from 0 through 15. An eight-bit register holds an integer from 0 through 127.

We see that the most natural way of specifying the contents of a register leaves no room for negative numbers. The representation of negative numbers will be discussed in the next section.

# 3.5.4 Bit Significance

Because binary numbers are used to describe the contents of registers and memory locations, the numerical concept of a *significant digit* is useful in singling out individual bits of a specific storage location. For example, if a four-bit register holds the binary number 1100, then the four digits in order of significance are 1, 1, 0, and 0. So the most significant digit is 1, and the least significant digit is 0. The three most significant digits are 110. The three least significant digits are 100. Sometimes in this text, the most significant bits will be referred to as the *top* or *upper* bits and the least significant as the *bottom* or *lower* bits.

# 3.6 Negative Number Representation

The customary way to represent a negative number is to prepend a minus sign. Putting a - in front of a 3 makes a -3. This method of representing negatives is called *signed magnitude* representation. It can be implemented on the computer by allocating one bit of storage for a sign bit. To change the sign of a number that is stored using signed magnitude representation, one can simply flip the sign bit. Signed magnitude representation is not generally used for integers on the computer. The reason is that in order to do addition with signed magnitude representation, you need to do it the way it is taught to youngsters.

# 3.6.1 Signed Magnitude Addition

To add x and y:

Case I. If x and y are both positive, just add and make your answer positive.

Case II. If x and y are both negative, remove the negative signs, add the numbers, and tack a minus sign onto the result.

Case III. If x and y have different signs, subtract the smaller magnitude from the larger magnitude, and if the larger magnitude had a minus sign, then tack this onto the result.

Implementing signed magnitude addition with logic circuits on a chip would be a terrible waste of transistors.

# 3.6.2 Easy Addition

The method which is actually used with logic circuits to add x and y works like this:

Pay no attention to whether x and y are positive or negative; just add them!

Such a method would seem to be no method at all. But it works. It works because a special system for representing negatives is used, and because a register has a finite size, like an odometer.

# 3.6.3 Odometer Arithmetic

An odometer is an adding machine. It adds up the miles that you drive. Mileage is always considered to have a positive value. (Would a negative value imply driving backwards, or what?) However, consider the following equation, which we would ordinarily think of as making sense only for negative numbers.