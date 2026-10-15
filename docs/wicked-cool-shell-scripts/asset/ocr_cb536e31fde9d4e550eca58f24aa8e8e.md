The last check, at ⑨ is whether the user specified just a minus sign and a decimal point (which would be pretty peculiar, you have to admit). All good? Then the script returns 0, indicating that the user input a valid float.

# Running the Script

If no error message is produced when the function is called, the return code is 0, and the number specified is a valid floating-point value. You can test this script by appending the following few lines to the end of the code:

```
if validfloat $1 ; then
 echo "$1 is a valid floating-point value."
fi

exit 0
```

If validint is generating an error, make sure that you have it in your PATH as a separate function accessible to the script or just copy and paste it into the script file directly.

# The Results

The validfloat shell script simply takes an argument to attempt to validate. Listing 1-13 uses the validfloat script to validate a few inputs.

```
$ validfloat 1234.56
1234.56 is a valid floating-point value.
$ validfloat -1234.56
-1234.56 is a valid floating-point value.
$ validfloat -.75
-.75 is a valid floating-point value.
$ validfloat -.12
Invalid floating-point number: '.' not allowed after decimal point.
$ validfloat 1.0344e22
Invalid number format! Only digits, no commas, spaces, etc.
```

Listing 1-13: Testing the validfloat script

If you see additional output at this point, it might be because you added a few lines to test out validint earlier but forgot to remove them when you moved on to this script. Simply go back to Script #5 on page 23 and ensure that the last few lines that let you run the function as a standalone are commented out or deleted.

# Hacking the Script

A cool additional hack would be to extend this function to allow scientific notation, as demonstrated in the last example. It wouldn't be too difficult. You'd test for the presence of 'e' or 'E' and then split the result into three