# Chapter 12. Writing a Tcl Extension

```
* Results:
* A standard Tcl result.
*
* Side effects:
* Creates a hash table.
* Adds new commands
* Creates new Tcl global variables for demo_version and
* demoInit_revision.
*--------------------------------------------------------------------------------------
```

```
int Demo_Init(Tcl_Interp *interp) {
    /* interp      Current interpreter. */
    /* 1
     * If this application will need to save any
     * data in a hash table initialize the hash table.
     */
    Demo_InitHashTable();
    /* 2
     * Call Tcl_CreateCommand for commands defined by this
     * extension
     */
    Tcl_CreateObjCommand(interp, "demo", Demo_Cmd,
        (ClientData) NULL, NULL);
    /* 3
     * Define the package for pkg_mkIndex to index
     */
    Tcl_PkgProvide(interp, "demo", DEMO_VERSION);
    /* 4
     * Define the version for this package
     */
    Tcl_SetVar((Tcl_Interp *) interp, "demo_version",
        DEMO_VERSION, TCL_GLOBAL_ONLY);

```

478