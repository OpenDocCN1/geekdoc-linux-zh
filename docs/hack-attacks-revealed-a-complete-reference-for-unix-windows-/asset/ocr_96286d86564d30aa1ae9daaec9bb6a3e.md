```
if (_AX==0)
{
    return 0;
}
XMSHandle=_DX;
return 1;
}
```

DOS does not automatically free allocated extended memory. A program using extended memory must release it before terminating. This function frees a block of extended memory previously allocated by AllocXMS:

```
void XMS_free(void)
{
    /*
       Free used XMS
    */
    _DX=XMSHandle;
    _AH=0x0A;
    (*XMSFunc)();
}
```

Two functions are now given: one for writing data to extended memory and one for reading data from extended memory into conventional memory:

```
/*
    XMSParms is a structure for copying information to and from
    real-mode memory to XMS memory
*/

struct parmstruct
{
    /*
       blocklength is the size in bytes of block to copy
    */
    unsigned long blockLength;

    /*
       sourceHandle is the XMS handle of source; 0 means that
       sourcePtr will be a 16:16 real-mode pointer, otherwise
       sourcePtr is a 32-bit offset from the beginning of the
       XMS area that sourceHandle points to
    */
    unsigned int sourceHandle;
    far void *sourcePtr;

    /*
       destHandle is the XMS handle of destination; 0 means that
       destPtr will be a 16:16 real-mode pointer, otherwise
```