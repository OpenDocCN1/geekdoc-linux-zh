The information provided here refers to an old version of SCO UNIX. If you require binaries for more recent SCO UNIX products, please contact SCO to obtain packages that are ready to install. You should also verify with SCO that your platform is up to date for the binary packages you will install. This is important if you wish to avoid data corruption problems with your installation. To build Samba for SCO UNIX products may require significant patching of Samba source code. It is much easier to obtain binary packages directly from SCO.

# ### 41.3 DNIX

DNIX has a problem with seteuid() and setegid(). These routines are needed for Samba to work correctly, but they were left out of the DNIX C library for some reason.

For this reason Samba by default defines the macro NO\_EUID in the DNIX section of includes.h. This works around the problem in a limited way, but it is far from ideal, and some things still will not work right.

To fix the problem properly, you need to assemble the following two functions and then either add them to your C library or link them into Samba. Put the following in the file seteuid.s:

```
          .globl    _setegid
_setegid:
           moveq   #47,d0
           movl    #100,a0
           moveq   #1,d1
           movl    4(sp),a1
           trap    #9
           bccs    1$
           jmp     cerror
1$:           clr1  d0
           rts
```

Put this in the file seteuid.s:

```
          .globl    _seteuid
_seteuid:
           moveq   #47,d0
           movl    #100,a0
           moveq   #0,d1
           movl    4(sp),a1
           trap    #9
           bccs    1$
           jmp     cerror
```