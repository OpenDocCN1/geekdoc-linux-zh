In this form, statements are executed once for each value in list, and for each iteration, the current value of list is assigned to curvar.

Suppose you want to create a backup version of each file in a sub directory called backup. You can do the following in pdsh and bash:

```
#!/bin/sh
for filename in *

  cp $filename backup/$filename
  if [ $ -ne 0 ]; then
    echo "copy for $filename failed"
  fi
done
```

In the preceding example, a backup copy of each file is created. If the copy fails, a message is generated.

The same example in tcsh is follows:

```
#!/bin/tcsh
foreach filename (`/bin/ls`)
  cp $filename backup/$filename
  if ($? != 0) then
    echo "copy for $filename failed"
  endif
```

# The while Statement

The while statement can be used to execute a series of commands while a specified condition is true. The loop terminates as soon as the specified condition evaluates to false. It is possible that the loop will not execute at all if the specified condition initially evaluates to false. You be careful with the while command because the loop will never terminate if the specified condition evaluates to false.

> Endless Loops Have Their Place in Shell Programs

Endless loops can sometimes be useful. For example, you can easily construct a simple command that constantly monitors 802.11b link quality of a network interface by using a few lines of script:

```
#!/bin/sh
while
  /sbin/iwconfig eth0 | fgrep Link | tr '\n' '\r'
done
```