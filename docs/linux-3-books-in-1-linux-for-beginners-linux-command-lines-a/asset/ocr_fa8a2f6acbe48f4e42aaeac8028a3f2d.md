```
```
*)
echo "Neither 100 nor 200";;
esac
```
```

The conditions go in between two keywords – case and esac. And we use \*)

to match all the inputs that are not 100 or 200.

# ### How to Use Command Line Arguments

There are several reasons why you might want to get an argument straight

from the command shell, and the next example demonstrates how you do this

using bash shell:

```
```
#!/bin/bash
echo "Total arguments : $#"
echo "First Argument = $1"
echo "Second Argument = $2"
```
```

Run the script with an extra two parameters following the name. The script is

saved as test.sh, and you can see the calling procedure here:

```
```
$ ./test.sh Hey Howdy
$1 accesses the first argument while $2 does the second and so on. We use $# to get the total argument number.
```
```

# ### How to Use Names to Get Arguments

The next example demonstrates how you can use their names to get the

command line arguments:

```
```
#!/bin/bash
for arg in "$@"
do
index=$(echo $arg | cut -f1 -d=)
val=$(echo $arg | cut -f2 -d=)
case $index in
X) x=$val;;
Y) y=$val;;
\*)
esac
done
((result=x+y))
echo "X+Y=$result"
```
```

Save and call this script test.sh and call it like this:

```
```
$ ./test.sh X=44 Y=100
```
```

You should see a return of X+Y=144. We store the arguments in '$@' and

then use the cut command in Linux to get them.