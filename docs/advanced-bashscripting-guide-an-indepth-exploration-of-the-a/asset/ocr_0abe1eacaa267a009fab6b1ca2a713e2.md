# Advanced Bash–Scripting Guide

dc uses RPN (“Reverse Polish Notation”).

Of the two, bc seems more useful in scripting. It is a fairly well-behaved UNIX utility, and may be used in a pipe.

Bash can't handle floating point calculations, and it lacks operators for certain important mathematical functions. Fortunately, bc comes to the rescue.

Here is a simple template for bc to calculate a script variable. This uses command substitution.

```
variable=$(echo "OPTIONS; OPERATIONS" | bc)
```

Example 12–30. Monthly Payment on a Mortgage

```
#!/bin/bash
# monthlypayment.sh: Calculates monthly payment on a mortgage.

# This is a modification of code in the "mcalc" (mortage calculator) package,
# by Jeff Schmidt and Mendel Cooper (yours truly, the author of this document).
# http://www.ibiblio.org/pub/Linux/apps/financial/mcalc-1.6.tar.gz [15k]
echo
echo "Given the principal, interest rate, and term of a mortgage,"
echo "calculate the monthly payment."

bottom=1.0
echo
echo -n "Enter principal (no commas) " 
read principal
echo -n "Enter interest rate (percent) " # If El,12%, enter "12", not ".12".
read interest_r
echo -n "Enter term (months) " 
read term

interest_r=$(echo scale=9; $interest_r/100.0" | bc) # Convert to decimal.
# scale determines how many decimal places.

interest_rate=$(echo scale=9; $interest_r/12 + 1.0" | bc)

top=$(echo scale=9; $principal*$interest_rate$term" | bc)
echo; echo "Please be patient. This may take a while."

let months=$term - 1
for ((x=$months; x > 0; x--));
do
bot=$(echo scale=9; $interest_rate^$x" | bc)
bottom=$(echo scale=9; $bottom+$bot" | bc)
# bottom = $(($bottom +bot))
done

# let payment = $top/$bottom
payment=$(echo scale=2; $top/$bottom" | bc)
```

# 12.7. Terminal Control Commands