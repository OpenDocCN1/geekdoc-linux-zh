# 1424

# tnfract

```
2455.215768 0.004457 6280 1 - inloop loop_count: 0x1
ntotal_iterations: 0x1
2455.217041 0.001273 6280 1 - inloop loop_count: 0x2
total_iterations: 0x2
2455.218285 0.001244 6280 1 - inloop loop_count: 0x3
total_iterations: 0x3
2455.219600 0.001315 6280 1 - inloop loop_count: 0x4
total_iterations: 0x4
4058.815125 1603.595525 6280 1 - inloop loop_count: 0x0
total_iterations: 0x5
4058.816699 0.003574 6280 1 - inloop loop_count: 0x1
total_iterations: 0x6
4058.819331 0.001232 6280 1 - inloop loop_count: 0x2
total_iterations: 0x7
4058.821264 0.001333 6280 1 - inloop loop_count: 0x3
total_iterations: 0x8
4058.822520 0.001256 6280 1 - inloop loop_count: 0x4
total_iterations: 0x9
4058.823781 0.001261 6280 1 - inloop loop_count: 0x5
total_iterations: 0xa
4058.825037 0.001256 6280 1 - inloop loop_count: 0x6
total_iterations: 0xb
13896.655540 9837.830413 6280 1 - final loop_count16: 0x258
total_iterations8: 0xb0
```

```
example%
```

Notice that the loop_count and the total_iterations are TNF unsigned arguments. Their values are printed in hexadecimal when requested by option -x.

# Exit Status

```
tnfdumpd returns 0 on successful exit.
```

# Attributes

See attributes(5) for descriptions of the following attributes:

| Attribute Type | Attribute Value |
| --- | --- |
| Availability | SUNWntfd |

# See Also

```
prex(1), getftime(3C), TNF_DECLARE_RECORD(3TNF), TNF_PROBE(3TNF),
tnf_process_disable(3TNF), attributes(5)
```

# Tnfxract — Extract Kernel Probes Output into a Trace File

# Synopsis

```
/usr/bin/tnfxtract -d dumpfile -n namelist] tnf_file
```