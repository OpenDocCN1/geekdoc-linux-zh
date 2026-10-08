.f .r~  
.r .r~

# Double Suffix Rules

+   .C.O  .C~.O  .C~.C  .C.a  .C~.a
.C.o  .C~.o  .C~.C  .C.a  .C~.a
.CXX.o  .CXX~.o  .CXX~.cXX  .CXX.a  .CXX~.a
.cpp.o  .cpp~.o  .cpp~.cpp  .cpp.a  .cpp~.a
.cc.o  .cc~.o  .cc~.CC  .cc.a  .cc~.a
.s.o  .S~.o  .S~.a
.P.o  .P~.o  .P~.p  .P.a  .P~.a
.f.o  .f~.o  .f~.f  .f.a  .f~.a
.r.o  .R~.o  .R~.r  .r.a  .r~.a
.y.o  .Y~.o  .Y~.y  .y.c
.l.o  .l~.o  .l.c
.h~-.h  .H~.h  .hxx~.hxx  .hpp~.hpp
.C.o  .C~.o  .C.a  .C~.a

Double suffix inference rules (.c.o) define how to build x.o from x.c.  
Single suffix inference rules (.c) define how to build x from x.c. In effect, the first suffix is null. Single suffix rules are useful for building targets from only one source file; e.g., shell procedures and simple C programs.

A tilde in the above rules refers to an SCCS file (see sccsfile(4)). Thus, the rule .C~.o would transform an SCCS C source file into an object file (.o). Since the s. of the SCCS files is a prefix, it is incompatible with make's suffix point-of-view. Hence, the tilde is a way of changing any file reference into an SCCS file reference.

A rule to create a file with suffix .o from a file with suffix .c is specified as an entry with .c.o as the target and no dependents. Shell commands associated with the target define the rule for making a .o file from a .c file. Any target name that has no slashes in it and starts with a dot is identified as an inference (implicit) rule instead of a target (explicit) rule. Targets with one dot are single suffix inference rules; targets with two dots are double suffix inference rules. Users can, in a Makefile, define additional inference rules and either redefine or cancel default inference rules.

The default inference rule for changing a .c file into a .o file might look like this:

```
```
.c.o:
	$(CC) $(CFLAGS) -c $<
```
```

and the default inference rule for changing a yacc file to a C object file might look like this:

```
```
.y.o:
	$(YACC) $(YFLAGS) $<
	$(CC) $(CFLAGS) -c y.tab.c
	rm y.tab.c
	mv y.tab.o $@
```
```

Certain macros are used in the default inference rules to permit the inclusion of optional matter in any resulting commands. For example, CFLAGS, LDFLAGS, and YFLAGS are used for compiler options to cc(1), lex(1), and yacc(1), respectively. LDFLAGS is commonly used to designate linker/loader options. These macros are automatically defined by make but can be redefined by the user in the Makefile.

The macro LIBS is, by convention, used to specify the order of inclusion of any special libraries during the linking phase of compilation. To specify a particular order of inclusion for a