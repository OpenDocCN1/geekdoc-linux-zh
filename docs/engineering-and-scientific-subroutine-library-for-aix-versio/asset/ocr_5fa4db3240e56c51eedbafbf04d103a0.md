save. This step is used, along with step 8, for ERRSTR. For information on whether you should use ERRSAV and ERRSTR, see “How Can You Control Error Handling in Large Applications by Saving and Restoring Entries in the Error Option Table?” on page 52. For an example, see “Example” on page 154, as the use is the same as for computational errors.

# Step 5. Call ERRSET:

```
errset(ierno,inoal,inomes,itrace,iusadr,i range);
```

This calls the ERRSET subroutine, which allows you to dynamically modify the action taken when an error occurs. For optionally-recoverable ESSL input-argument errors, you need to call ERRSET only if you want to avoid terminating your program and you want the input arguments associated with this error to be assigned correct values in your program when the error occurs. For one error (ierno) or a range of errors (i range), you can specify:

+   - How many times each error can occur before execution terminates (inoal)
+   - How many times each error message can be printed (inomes)
+   - The ESSL exit routine ENOTRM, to be invoked for the error indicated (iusadr)

ERRSET must be called for each error code you want to indicate as being recoverable. For ESSL, ierno should have a value of 2015, 2030, or 2200. If you want to eliminate error messages, you should indicate a negative number for inomes; otherwise, you should specify 0 for this argument. All the other ERRSET arguments should be specified as 0.

For a list of the default values set in the ESSL error option table, see Table 29 on page 50. For a description of the input-argument errors, see “Input-Argument Error Messages(2001-2099)” on page 176. For a description of ERRSET, see Chapter 17, ‘Utilities,’ on page 951.

# Step 6. Call ESSL:

```
irc = name(arg1, ..., argn);
if irc == rc1
{
.
.
.
}
if irc == rc2
{
.
.
.
}
```

This calls the ESSL subroutine and specifies a branch on one or more return code values, where:

+   - name specifies the ESSL subroutine.
+   - arg1, ..., argn are the input and output arguments.
+   - irc is the integer variable containing the return code resulting from the computation performed by the ESSL subroutine.