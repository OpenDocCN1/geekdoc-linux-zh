# make 805

| Use | Implicit Rule | Command Line |
| --- | --- | --- |
| NeWS files | .cps.h | $ (RM) $* |
| | .cps-.h | cps $*.cps |
| | | $ (GET) $ (CFLAGS) -p $ > *.cps |
| | | $ (CPS) $ (CFLAGS) $.* |
| Pascal files | .p | $ (LINK.p) -o $ < $ (LDLIBS) |
| | .p.o | $ (COMPILE.p) $ (OUTPUT_OPTION) $< |
| | .p~ | $ (GET) $ (CFLAGS) -p $ > *.p |
| | | $ (LINK.p) -o $*.p $ (LDLIBS) |
| | | $ (GET) $ (CFLAGS) -p $ > *.p |
| | | $ (COMPILE.p) $ (OUTPUT_OPTION) $*.p |
| | .p~a | $ (GET) $ (CFLAGS) -p $ > *.p |
| | | $ (COMPILE.p) -o % $*.p |
| | | $ (AR) $ (ARFLAGS) $@ $% |
| | | $ (RM) $ |
| Ratfor files | .r | $ (LINK.r) -o $ < $ (LDLIBS) |
| | .r.o | $ (COMPILE.r) $ (OUTPUT_OPTION) $< |
| | .r.a | $ (COMPILE.r) -o % $< |
| | | $ (AR) $ (ARFLAGS) $@ $% |
| | | $ (RM) $ |
| | .r~ | $ (GET) $ (CFLAGS) -p $ > *.r |
| | | $ (LINK.r) -o $*.r $ (LDLIBS) |
| | .r~o | $ (GET) $ (CFLAGS) -p $ > *.r |
| | | $ (COMPILE.r) $ (OUTPUT_OPTION) $*.r |
| | .r~a | $ (GET) $ (CFLAGS) -p $ > *.r |
| | | $ (COMPILE.r) -o % $*.r |
| | | $ (AR) $ (ARFLAGS) $@ $% |
| | | $ (RM) $ |
| SCCS files | .SCCS_GET | sccs $ (SCCSFLAGS) get $ (SCCSFLAGS) $@ |
| | | -GS |
| | .SCCS_GET_POSIX | sccs $ (SCCSFLAGS) get $ (SCCSFLAGS) $@ |
| | .GET_POSIX | $ (GET) $ (CFLAGS) s$. |
| Shell scripts | .sh | cat $< > $@ |
| | chmod +x $ | |
| | sh~ | $ (GET) $ (CFLAGS) -p $ > *.sh |