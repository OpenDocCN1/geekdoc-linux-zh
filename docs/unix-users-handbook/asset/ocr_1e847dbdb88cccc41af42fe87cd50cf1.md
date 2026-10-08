```
0 0 100 0 0 0
```

4. Replace the page reclams and address translation faults with process swapping in the default output.

```
vstat -S
```

| procs | faults | memory | page |
| :--- | :--- | :--- | :--- |
| cpu | | | |
| r b w avm free si so pi po fr de sr |
| in sy cs us sy id |
| 0 0 0 1158 430 0 0 0 0 0 0 0 |
| 111 18 7 0 0 100 |

5. Display the default output twice at five-second intervals. Note that the headers are not repeated.

```
vstat 5 2
```

| procs | faults | memory | page |
| :--- | :--- | :--- | :--- |
| cpu | | | |
| r b w avm free re at pi po fr de sr |
| in sy cs us sy id |
| 0 0 0 1158 456 0 0 0 0 0 0 0 |
| 111 18 7 0 0 100 |
| 0 0 0 1221 436 5 0 5 0 0 0 0 |
| 108 65 18 0 1 99 |

6. Display the default output twice in 80-column format at five-second intervals. Note that the headers are not repeated.

```
vstat -n 5 2
```

| VM |
| :--- |
| memory | faults |
| avm free re at pi po fr de sr in sy cs |
| 1221 436 0 0 0 0 0 0 0 111 18 7 |
| CPU |
| cpu | procs |
| us sy id r b w |
| 0 0 100 0 0 0 |
| 1221 435 2 0 2 0 0 0 0 109 35 17 |
| 0 1 99 0 0 0 |

7. Display the default output and disk transfers twice in 80-column format at five-second intervals. Note that the headers are repeated.

```
vstat -dn 5 2
```

| VM |
| :--- |
| memory | page | faults |
| avm free re at pi po fr de sr in sy cs |
| 1221 435 0 0 0 0 0 0 0 111 18 7 |
| CPU |
| cpu | procs |
| us sy id r b w |
| 0 0 100 0 0 0 |

Disk Transfers

| device | xfer/sec |
| :--- | :--- |
| c0t6d0 | 0 |