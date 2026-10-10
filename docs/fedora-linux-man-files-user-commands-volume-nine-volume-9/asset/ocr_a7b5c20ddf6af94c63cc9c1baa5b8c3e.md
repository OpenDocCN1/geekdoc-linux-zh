# MODULI GENERATION

**ssh-keygen** may be used to generate groups for the Diffie-Hellman Group Exchange (DH-GEX) protocol. Generating these groups is a two-step process: first, candidate prs are generated using a fast, but more intensive process. These candidate prs are then tested for suitability (a CPU-intensive process).

Generation of prs is perford using the -G option. The desired length of the prs may be specified by the -b option. For example:

```
    # ssh-keygen -G moduli-2048.candidates -b 2048
```

By default, the search for prs begins at a random point in the desired length range. This may be overriden using the -S option, which specifies a different start point (in hex).

Once a set of candidates have been generated, they st be screened for suitability. This may be perford using the -T option. In this mode **ssh-keygen** will read candidates from standard input (or a file specified using the -f option). For example:

```
    # ssh-keygen -T moduli-2048 -f moduli-2048.candidates
```

By default, each candidate will be subjected to 100 primality tests. This may be overriden using the -a option. The DH generator value will be chosen automatically for the pri under consideration. If a specific generator is desired, it may be requested using the -W option. Valid generator values are 2, 3, and 5.

Screened DH groups may be installed in /etc/ssh/moduli It is important that this file contains moduli of a range of bit lengths and that both ends of a connection share common moduli.