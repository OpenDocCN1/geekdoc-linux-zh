```
done
return 0
}
```

2. The following command does the job:
$ uptime | sed 's/.* load/'

3. There are two possible solutions:
$ df -k | sed -n '/\/$/p'
$ df -k | sed '/^\/1/ d'

4. The following command will solve this problem:
/bin/ls -al | sed -e 's/^[^ ]*/-d' -e 's/*[0-9].* / /'

# Hour 17

1. A possible implementation is as follows:

```
#!/bin/sh
if [ $# -lt 1 ]; then
echo 'USAGE: `basename $0` files'
exit 1
fi
awk '{
for (i=NF;i>=1;--i) {
printf "%s ", $i ;
}
printf "\n" ;
}' $0
```

2. A possible solution is

```
#!/bin/sh
awk 'BEGIN { FS=":" ; }
$1 == "B" {
BAL+=SNF ; next ;
}
$1 == "D" {
BAL += SNF ;
}
{ $1 == "C" || $1 == "W" {
BAL-=SNF ;
}
{ $1 == "C" || $1 == "W" || $1 == "D" {
printf "%10s %8.2f\n",$2,BAL ;
}
}' account.txt ;
```