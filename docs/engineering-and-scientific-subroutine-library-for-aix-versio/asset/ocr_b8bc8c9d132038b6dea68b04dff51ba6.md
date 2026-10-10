```
DECLARE AN AREA TO SAVE THE  
ERROR OPTION TABLE INFORMATION  
FOR ERROR CODE 2101

```
CHARACTER*8 SAV2101
```

INITIALIZE THE ESSL ERROR  
OPTION TABLE

```
CALL EINFO(0)  
SAVE THE EXISTING ERROR OPTION  
TABLE ENTRY FOR ERROR CODE 2101
CALL ERRSAV(2101,SAV2101)
```

ALLOW 255 ERRORS FOR CODE 2101

```
CALL ERRSET(2101,255,0,0,0,2101)
```

CALL ESSL SUBROUTINE DGE EV.  
IF THE EIGENVALUE FAILED TO  
CONVERGE, CONTROL GOES TO LABEL 400

```
CALL DGE EV(IOPT,A, LDA ,N ,Z ,LDZ,SELECT,N,AUX ,NAUX ,*+00)
```

CALL THE INFORMATION-HANDLER  
ROUTINE FOR ERROR CODE 2101 TO  
RETURN TWO PIECES OF INFORMATION.  
VARIABLE I I CONTAINS THE EIGENVALUE  
THAT FAILED TO CONVERGE. VARIABLE  
I2 CONTAINS THE NUMBER OF ITERATIONS.

```
400 CALL EINFO (2101,I1,I2)
```

RESTORE THE PREVIOUS ERROR OPTION  
TABLE ENTRY FOR ERROR CODE 2101.  
ERROR PROCESSING RETURNS TO HOW IT  
WAS BEFORE IT WAS ALTERED BY THE ABOVE  
ERRSET STATEMENT.

```
CALL ERRSTR(2101,SAV2101)
```
```

# Example of Handling Errors in a Multithreaded Application  
Program

This 32-bit environment example shows how to modify the MATINV_EXAMPLE  
program in “Creating Multiple Threads and Calling ESSL from Your Fortran  
Program” on page 113 with calls to the ESSL error handling subroutines. The ESSL  
error handling subroutines are called from each thread to: initialize the error  
option table, save the current error option table values for input-argument error  
2015 and computational error 2105, change the default values for errors 2015 and  
2105, and then restore the original default values for errors 2015 and 2105.