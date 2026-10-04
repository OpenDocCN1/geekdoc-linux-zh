# Chapter 12. Writing a Tcl Extension

```
Tcl_ObjGetVar2(interp, objv[2], indexPtr, 0);

if (structElementPtr == NULL) {
    Tcl_AppendResult(interp,
        Array "", fields[i],
        "" is not defined ", (char *) NULL);
    returnStructPtr->status = TCL_ERROR;
    goto done;
}
/*
* This is a strange way to determine which structure
* element is being processed, but it works in the loop.
*
* If an illegal value is in the object, the error
* return will be set automatically by the interpreter.
*/
switch (i) {
case 0: {
    int t;
    if (TCL_OK !=
        Tcl_GetIntFromObj(interp,
            structElementPtr, &t)) {
        returnStructPtr->status = TCL_ERROR;
        goto done;
    } else {
        demoStruct.firstIn = t;
    }
    break;
}
case 1: {
    char *t;
    if (NULL == (t =
        Tcl_GetStringFromObj(structElementPtr,
            NULL())))) {
        returnStructPtr->status = TCL_ERROR;
        goto done;
    } else {
        demoStruct.secondString=
            (char *)malloc(strlen(t)+1);
        strcpy(demoStruct.secondString, t);
    }

```

506