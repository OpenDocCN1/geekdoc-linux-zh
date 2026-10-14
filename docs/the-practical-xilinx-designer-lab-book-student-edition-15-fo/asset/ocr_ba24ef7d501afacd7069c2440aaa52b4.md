# Figure 4.21 The XSE.VHD file has been added to the xse library.

The ENTITY section of the 8-bit adder is named byteadd on line 9. The PORT statement declares two 8-bit addend inputs (a and b) and a carry input (cin) on lines 11 through 13. These are followed by the declaration of an 8-bit summation output (sum) and a carry output bit (cout) on lines 14 and 15.

The ARCHITECTURE section starts on line 20. Note that there is no need for the byteadd module to use a COMPONENT statement to gain access to the full-adder bit. This has already been taken care of by accessing the xse library on lines 4 through 6.

The byteadd module could be written using 8 separate instantiations of the fulladd module to create an 8-bit adder. Instead, we use a FOR loop on line 26 to iteratively instantiate 8 copies of the fulladd module. The GENERATE and END GENERATE statements on lines 27 and 36 surround the instantiation of a fulladd module. The loop counter, i, is used to index the input and output arrays as the looping proceeds. For example, the first time through the loop the