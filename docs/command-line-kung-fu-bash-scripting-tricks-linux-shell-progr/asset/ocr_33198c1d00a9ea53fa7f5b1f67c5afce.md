# # Fix Common Typos with Aliases

```
$ alias typo='correct spelling'
```

If you find yourself repeatedly making the same typing mistake over and over, fix it with an alias.

```
$ grep root /etc/passwd
bash: grep: command not found
$ echo "alias grep='grep'" >> ~/.bash_profile
$ . ~/.bash_profile
$ grep root /etc/passwd
root:x:0:0:root:/root:/bin/bash
$ 
```

# ## Sort the Body of Output While Leaving the Header on the First Line Intact

Add this function to your personal initialization files such as ~/.bash_profile:

```
body() {
	IFS= read -r header
	printf '%s\n' "$header"
	"$@"
}
$ command | body sort
$ cat file | body sort
```