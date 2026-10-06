```
rmi:x118:100:127 /home/rmi:/bin/bash
vern:x119:100:201 /home/vern:/bin/bash
bob:x120:100:227 /home/bob:/bin/bash
janet:x122:100:227 /home/janet:/bin/bash
maggie:x124:100:244 /home/maggie:/bin/bash
dan:x26:100:229 /home/dan:/bin/bash
dave:x108:100:427 /home/dave:/bin/bash
mary:x129:100:303 /home/mary:/bin/bash
```

```
$ cat passwd_check
gawk </etc/passwd '
BEGIN {
	uid[0] = ""
	# tell gawk that uid is an array
}
{
	dup = 0
	# no password indicates process all records
	# initialize duplicate flag
	split($0, field, ":")
	# split into fields delimited by ":"
	if (field[2] == "") {
		# check for null password field
		if (field[5] == "") {
			# check for null info field
			print field[1] " has no password."
		}
	} else {
		print field[1] " ("field[5]") has no password."
	}
}
for (name in uid) # loop through uid
{
\tif (uid[name] == field[3]) # check for 2nd use of UID
		print field[1] " has the same UID as "name : UID = ""
		dup = 1 # set duplicate flag
	if (dup) # same as as: if (dup == 0)
	# assign UID and login name to uid array
	{
		uid[field[1]] = field[3]
	}
```

```
$ passwd_check
bill (ext 123) has no password.
toni (ext 357) has no password.
nail has the same UID as toni : UID = 164
dan has no password.
dave has the same UID as sales : UID = 108
```

(The pwck utility also performs these checks, as well as a few more.)
The final example shows a complete interactive shell script that uses gawk to generate a report: