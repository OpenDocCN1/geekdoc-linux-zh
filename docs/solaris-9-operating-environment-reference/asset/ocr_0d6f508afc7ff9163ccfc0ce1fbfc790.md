# 802

# make

| Use | Implicit Rule Name | Command Line |
| --- | --- | --- |
| FORTRAN 77 files | .f | $(LINK.f) -o $0 $@ $(LDLIBS) |
| | .f.o | $(COMPILE.f) $(OUTPUT_OPTION) $\$
| | .f.a | $(COMPILE.f) -o $ $ $
| | | $(AR) (ARFLAGS) $@0 $ $\$
| | | $(RM) $@ $ $\$
| | .f | $(LINK.f) -o $0 $@ $(LDLIBS) |
| | .f~ | $(GET) (GFLAGS) -p $ > *.f |
| | | $(FC) (FFLAGS) (LDFLAGS) -o $ $@ *.f |
| | .f~o | $(GET) (GFLAGS) -p $ > *.f |
| | | $(FC) (FFLAGS) -c *.f |
| | .f~a | $(GET) (GFLAGS) -p $ > *.f |
| | | $(COMPILE.f) -o $ *.f |
| | | $(AR) (ARFLAGS) $@0 $ $\$
| | | $(RM) $@ $ $\$
| | .F | $(LINK.F) -o $ $@ $(LDLIBS) |
| | .F.o | $(COMPILE.F) -o $ $(OUTPUT_OPTION) $\$
| | .F.a | $(COMPILE.F) -o $ $ $\$
| | | $(AR) (ARFLAGS) $@0 $ $\$
| | | $(RM) $@ $ $\$
| | .F~ | $(GET) (GFLAGS) -p $ > *.f |
| | | $(FC) (FFLAGS) (LDFLAGS) -o $ $@ *.f |
| | .F~o | $(GET) (GFLAGS) -p $ > *.f |
| | | $(FC) (FFLAGS) -c *.f |
| | .F~a | $(GET) (GFLAGS) -p $ > *.f |
| | | $(COMPILE.F) -o $ *.f |
| | | $(AR) (ARFLAGS) $@0 $ $\$
| | | $(RM) $@ $ $\$
| FORTRAN 90 files | .f90 | $(LINK.f90) -o $ $@ $ $(LDLIBS) |
| | .f90~ | $(GET) (GFLAGS) -p $ > *.f90 |
| | | $(LINK.f90) -o $ $@ *.f90 $(LDLIBS) $\$
| | .f90.o | $(COMPILE.f90) $(OUTPUT_OPTION) $\$
| | .f90~o | $(GET) (GFLAGS) -p $ > *.f90 |