# 514 Lab 11.2: The exec Command

```
exec 3 < "\${inFiles[0]}"
exec 4 < "\${inFiles[1]}"
```

read outputFile?"Where do you want the shuffled output? "
exec 5 > "$outFile"

```
IFS=
while read -ru3
  do
    print -u5 "$REPLY"
    read -ru4
    print -u5 "$REPLY"
done
IFS=$' '\t\n'
  exec 3<&-
  exec 4<&-
  exec 5<&-
done
print
```

f) What are four things the user could type to cause this script to stop executing?

g) What is the purpose of the print command at the end of the script?