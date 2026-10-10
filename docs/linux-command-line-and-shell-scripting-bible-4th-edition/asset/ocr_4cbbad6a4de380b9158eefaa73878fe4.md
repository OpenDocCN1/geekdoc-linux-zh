```
/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin/
$
```

The `ENVIRON["HOME"]` variable retrieves the HOME environment variable value from the shell. Likewise, the `ENVIRON["PATH"]` variable retrieves the PATH environment variable value. You can use this technique to retrieve any environment variable value from the shell to use in your *gawk* programs.

The *FNR*, *NF*, and *NR* variables come in handy when you're trying to keep track of data fields and records in your *gawk* program. Sometimes you're in a situation where you don't know exactly how many data fields are in a record. The *NF* variable allows you to specify the last data field in the record without having to know its position:

```
$ gawk 'BEGIN{FS=";"; OFS=""} {print $1,$NF}' /etc/passwd
root::/bin/bash
daemon:/usr/sbin/nologin
bin:/usr/sbin/nologin
sys:/usr/sbin/nologin
sync:/bin/sync
games:/usr/sbin/nologin
man:/usr/sbin/nologin
...
rich:/bin/bash
$
```

The *NF* variable contains the numerical value of the last data field in the data file. You can then use it as a data field variable by placing a dollar sign in front of it.

The *FNR* and *NR* variables are similar to each other but slightly different. The *FNR* variable contains the number of records processed in the current data file. The *NR* variable contains the total number of records processed. Let’s look at a couple of examples to see this difference:

```
$ gawk 'BEGIN{FS=","}{print $1,"FNR="FNR}' data1 data1
data11 FNR=1
data21 FNR=2
data31 FNR=3
data11 FNR=1
data21 FNR=2
data31 FNR=3
$
```