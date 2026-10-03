# Hack 97. vmstat Command

For a typical performance monitoring all you need is only vmstat command.
This display memory, swap, IO, system and cpu performance information.
The following command executes vmstat every 1 second for 100 times.

```
# vmstat 1 100
```

```
procs ------memory----- -swap- ---io--- -system-- --cpu--
r b swpd free buff cache si so
0 0
0 0
0 282120 134108 5797012
0 282120 134108 5797012
126
0
0
bi
0
0
bo in
0
0
2
0
cs us sy id wa
0 0 0 100 0
0 1007 359 0 0 100 0
```