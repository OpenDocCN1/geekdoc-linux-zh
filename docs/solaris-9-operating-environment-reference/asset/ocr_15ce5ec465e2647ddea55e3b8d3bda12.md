# 804 make

# Use Implicit Name Command Line

.1~ $(COMPILE.C) -o $@ $*.c
$(RM) *.c
$(GET) $(GFLAGS) -p $ > $*.1
$(LEX) $(LFLAGS) *.1
$(CC) $(CFLAGS) -c lex.yy.c
rm -f lex.yy.c
mv lex.yy.c $@

.1~.c $(GET) $(GFLAGS) -p $ > $*.1
$(LEX) $(LFLAGS) *.1
mv lex.yy.c $@

.1~.ln $(GET) $(GFLAGS) -p $ > $*.1
$(RM) *.c
$(LEX.1) $*.1 > $*.c
$(LINT.c) -o $@ -i $*.c
$(RM) *.c

.1~.o $(GET) $(GFLAGS) -p $ > $*.1
$(LEX) $(GFLAGS) *.1
$(CC) $(CFLAGS) -c lex.yy.c
rm -f lex.yy.c $@

Module 2 files .mod $(COMPILE.mod) -o $@ -e $@ $$
.mod.o $(COMPILE.mod) -o $ $<
.def.sym $(COMPILE.def) -o $@ $$
def~.sym $(GET) $(GFLAGS) -p $ > $*.def
$(COMPILE.def) -o $@ $*.def
.mod~ $(GET) $(GFLAGS) -p $ > $*.mod
$(COMPILE.mod) -o -e $@ $*.mod

mod~.o $(GET) $(GFLAGS) -p $ > $*.mod
$(COMPILE.mod) -o $@ $*.mod
mod~.a $(GET) $(GFLAGS) -p $ > $*.mod
$(COMPILE.mod) -o $% $*.mod
$(AR) $(ARFLAGS) $@ *Tinh $@