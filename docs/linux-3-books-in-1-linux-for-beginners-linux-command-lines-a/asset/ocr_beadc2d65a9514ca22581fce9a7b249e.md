```
$ cat test15567
#!/bin/bash
function Myfunction1 {
  echo "You are looking at the example of a Linux shell function."
}
count=1
while [ $count -le 10 ]
do
  Myfunction1
  count=$[ $count + 1 ]
done
  echo "You have reached the end of the loop."
  Myfunction1
  echo "This is the finising point of your Linux shell script. Where do you want to go now?"
**Bash -f main.sh**
```

You are looking at the example of a Linux shell function.

You are looking at the example of a Linux shell function.

Repeated eight more times, until the final line of:

You have reached the end of the loop.

You are looking at the example of a Linux shell function.

This is the finising point of your Linux shell script. Where do you want to
go now?

When the name, Myfunction1, is referred to, the bash shell returns its
definition and the commands defined in it are executed. The definition does
not need to be first in the shell script but if you try using a function before the
definition, an error message is thrown:

```
$ cat test15567
#!/bin/bash
count=1
echo "You are seeing this line that comes before the function definition."

function Myfunction1 {
  echo "You are looking at the example of a Linux shell function."
}

while [ $count -le 10 ]
do
  Myfunction1
  count=$[ $count + 1 ]
done
  echo "You have reached the end of the loop."
  function Myfunction2
  echo "This is a definition of another function"
**Bash -f main.sh**
```