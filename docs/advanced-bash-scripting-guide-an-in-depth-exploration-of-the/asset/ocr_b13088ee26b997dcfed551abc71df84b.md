# Advanced Bash-Scripting Guide

```
# **************************************************
# Pack a variable
## with all the space-separated elements of the original array.
# Attempting to just pass the array itself will not work.

# This is the trick that allows grabbing an array as a "return value".
# *****************************************************
returned_array=$(Pass_Array "$argument") 
# *****************************************************
# Assign 'echoed' output of function to array variable.

echo "returned_array" ${returnedreturned_array[@]}
echo ""

# Now, try it again,
## attempting to access (list) the array from outside the function.
Pass_Array "$argument"

# The function itself lists the array, ...
## accessing the array from outside the function is forbidden.
echo "Passed array" = ${passed_array[@]}
# NULL VALUE since the array is a local variable to the function.
echo
####################################################

# And here is an even more explicit example:
ret_array() {
	for element in {1..20};
	do
		echo "$element " # Echo individual elements
		## of what will be assembled into array.
	done}
arr=$(ret_array) # Assemble array.
echo "Capturing array \"arr\" from function ret_array () ..."
echo "third element of array \"arr\" is ${arr[2]}." # 13 (zero-indexed)
echo -n "Entire array is: "
echo ${arr[@]}
#	# 11 12 13 14 15 16 17 18 19 20
echo
exit 0

# Nathan Coulter points out that passing arrays with elements containing
## whitespace breaks this elaborate example.
For a more elaborate example of passing arrays to functions, see Example A-10.
```

+   - Using the double-parentheses construct, it is possible to use C-style syntax for setting and incrementing/decrementing variables and in for and while loops. See Example 11-13 and Example 11-18.

Chapter 36. Miscellany

536