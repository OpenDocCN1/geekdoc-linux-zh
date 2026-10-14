# Listing 4.7  8-bit adder VHDL code modified to get an input through the MD0 pin of the XC4005XL FPGA. (Cont’d.)

```
038- input0=>a(i),
039- input1=>b(i), -- connect to intermediate bus bit
040- carry_input=>c(i),
041- sum=>sum(i),
042- carry_output=>c(i+1)
043- );
044- END GENERATE;
045- cout<=c(8);
046- END byteadd_arch;
```

MD0.XNF and MD2.XNF files into the directory of any project that requires the use of these pins. (But do not use the Document → Add... menu item to actually add them to your HDL mode project because this is not allowed.) The XNF for the other modules is usually stored in the Foundation Series software directory hierarchy in a place like Xilinx\Synth\xilinx\macros\Xc4000e\v6_xnf. You can also include schematic-based circuits into a VHDL design by exporting their XNF netlists from the Schematic Editor tool and then placing their inputs and outputs into COMPONENT statements.

# Listing 4.8  XNF file for the MD0 pin of the XC4005XL FPGA.

```
001- LCANET, 5
002- PROG, ACTIVE-CAD-2-XNF, 2.5.5.50, Sun Sep 13 11:53:37 1998
003- PART, 4000E
004- SYM, MD0, MD0, SCHNM=MD0, LIBVER=2.0.0
005- PIN, I, 0, MD0
006- END
007- EOF
```

Once the BYTEADD VHD file is complete and added to the ADD8_40 project in the XCPROJ-V directory, you can synthesize it for an XC4005XL FPGA. (Do not forget to select byteadd as the top-level module in the Top Level drop-down menu of the Synthesis/Implementation window.) Since the b(2) input is not used in Listing 4.7, the Foundation Series software does not synthesize this input into the netlist file. Therefore, you have to slightly modify the ADD8_40.UCF file so that the constraint on B<2> is removed or commented-out as follows:

```
NET CIN        LOC=P44;
NET A<0>       LOC=P45;
NET A<1>       LOC=P46;
NET A<2>       LOC=P47;
NET B<0>       LOC=P48;
NET B<1>       LOC=P49;
```