```
if(status==0x80)
{
 GetXMSEntry();
 
 XMSBuf = (char far *) farmalloc(BLOCKSIZE);
 if (XMSBuf == NULL)
 return 2;
 return 0;
}
return 1;
}

void GetXMSEntry(void)
{
 /*
 GetXMSEntry sets XMSFunc to the XMS Manager entry point
 so we can call it later
 */
 _AX=0x4310;
 geninterrupt(0x2F);
 XMSFunc = (void (far *)(void)) MK_FP (_ES, _BX);
}
```

Once the presence of extended memory has been confirmed, the following program can find out how much of it is available:

```
void XMSSize(int *kbAvail, int *largestAvail)
{
 /*
 XMSSize returns the total kilobytes available, and the size
 in kilobytes of the largest available block
 */
 _AH=8;
 (*XMSFunc)();
 *largestAvail=_DX;
 *kbAvail=_AX;
}
```

The next function may be called to allocate a block of extended memory, as you would allocate a block of conventional memory:

```
char AllocXMS(unsigned long numberBytes)
{
 /*
 Allocate a block of XMS memory numberBytes long
 Returns 1 on success
 0 on failure
 */
 
 _DX = (int)(numberBytes / 1024);
 _AH = 9;
 (*XMSFunc)();
```