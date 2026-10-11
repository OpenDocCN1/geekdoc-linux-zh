A paused domain is not completely shut down. The current state is saved and the execution of the domain can be continued with the **unpause** command:

```
xm unpause <domain_id>
```

To shutdown a domain, use the **shutdown** command:

```
xm shutdown <domain_id>
```

In case the domain is not responding anymore, you can force the shutdown of the domain with the **destroy** command:

```
xm destroy <domain_id>
```

To save the state of a domain for a longer time (e.g. over a reboot of domain0) you can use the **save** command:

```
xm save <domain_id> <filename>
```

The domain can be restored from the resulting file with the **restore** command:

```
xm restore <filename>
```

Another commonly used command is **mem-set**, which allows you to change the memory allocation of a domain:

```
xm mem_set <domain_id> <amount_of_memory>
```

The amount of memory is specified in megabytes.