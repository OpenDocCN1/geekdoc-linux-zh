
```
inPath () {
  OLDFIFS=$IFS
  IFS=:
  RC=1
  for i in $PATH
    do
      if [ -x "$i/$1" ] ; then
        echo "$i/$1"
        RC=0
        break
      fi
    done
  IFS=$OLDFIFS
  return $RC
}
```

![](img/3def70414996f811615f713b2077a154_462_0.png)

### 2. 一个可能的实现是

```
mymkdir() {

if [ $# -lt 1 ] ; then
 echo "ERROR: Insufficient arguments." >&2
 return 1
fi

mkdir -p "$1" > /dev/null 2>&1
if [ $? -eq 0 ] ; then
 cd "$1" 2>/dev/null
 if [ $? -eq 0 ] ; then
 pwd
 else
 echo "ERROR: Could not cd to $1." >&2
 fi
else
 echo "ERROR: Could not mkdir $1." >&2
fi
}
```

### 3. 你可以用对以下函数的调用替换第 2 题中的 mkdir -p：

```
mkdirp() {
OLDDIFS="$IFS"
IFS=/
for i in $1
do
 if [ -z "$i" ] ; then i="/" ; fi
 if [ -z "$parent" ] ; then
 parent="$i"
 elif [ "$parent" = "/" ] ; then
 parent="$parent$i"
 else
 parent="$parent/$i"
 fi
 if [ ! -d "$parent" ] ; then
 if [ ! -e "$parent" ] ; then
 mkdir "$parent"
 if [ $? -ne 0 ] ; then
 echo "mkdir $parent failed."
 IFS="$OLDDIFS"
 return 1
 fi
 else
 echo "$parent exists, but is not a dir."
 IFS="$OLDDIFS"
 return 1
 fi
 fi
fi
done
IFS="$OLDDIFS"
return 0
}
```

#### 4. 一个可能的解决方案是

```
readPass () {
  stty -echo
  while : ;
  do
    PASS1=""
    PASS2="Enter Password: "
    echo -n "Enter Password: "
    read PASS1
    if [ -z "$PASS1" ] ; then
      echo
      echo "Error: Password must not be blank. Try again." 1>&2
      fi
      continue
    fi
    echo -n "Enter Password (confirm): "
    read PASS2
    if [ "$PASS2" != "$PASS1" ] ; then
      echo
      echo "Error: Passwords do not match. Try again." 1>&2
      fi
      continue
    fi
    PASS="$PASS1"
    break;
  done;
  stty echo
  echo
}
```

#### 5. 一个可能的实现是

```
Prompt_RESPONSE() {
  if [ $# -lt 1 ] ; then
    echo "ERROR: Insufficient arguments." >&2
    return 1
  fi
  RESPONSE=
  while [ -z "$RESPONSE" ]
  do
    echo "$1\c "
    read RESPONSE
  done
  export RESPONSE
}
```

![](img/3def70414996f811615f713b2077a154_464_0.png)

## 第 15 小时

### 1. 一个示例实现是

```
ispids() {
  USAGE="usage: ispids [-h] process"
  HEADER=false
  PSCMD="/bin/ps -ef"
  case "$1" in
    -h) HEADER=true ; shift ;;
  esac
  if [ -z "$1" ] ; then
    echo $USAGE
    return 1
  fi
  if [ "$HEADER" = "true" ] ; then
    $PSCMD 2> /dev/null | head -n 1 ;
  fi
  $PSCMD 2> /dev/null | grep "$1" | grep -v grep
}
```

对于 Linux 或 FreeBSD，将变量 PSCMD 从

```
PSCMD="/bin/ps -ef*"
```

改为

```
PSCMD="/bin/ps -auxe*"
```

### 2. 以下是一个可能的实现：

```
ispids () {
  USAGE="usage: ispids [-h -s] process";
  HEADER=false;
  SORT=false;
  PSCMD="/bin/ps -efk";
  SORTCMD="sort -rnk 2,2";
  for OPT in $@;
  do
    case "$OPT" in
      -h)
        HEADER=true;
        shift
        ;;
      -s)
        SORT=true;
        shift
        ;;
```

```
*) 
echo $USAGE;
return 1
esac;
done;
if [ -z "$1" ]; then
echo $USAGE;
return 1;
fi;
if [ "$SHEADER" = "true" ]; then
$PSCMD | head -1;
fi;
if [ "$SORT" = "true" ]; then
$PSCMD 2> /dev/null | grep $1 | grep -v grep | $SORTCMD;
else
$PSCMD 2> /dev/null | grep $1 | grep -v grep;
fi
}
```

对于 Linux 和 FreeBSD，将变量 SORTCMD 改为

SORTCMD="sort -rn"

而不是

SORTCMD="sort -rn -k 2,2"

你还需要将变量 PSCMD 从

PSCMD="/bin/ps -ef"

改为

PSCMD="/bin/ps -auxw"

## 第16小时

- 1. 一种可能的实现是

```
sgrep() {
if [ $# -lt 2 ]; then
echo 'USAGE: sgrep pattern files' >&2
exit 1
fi
PAT="$1"; shift;
for i in $@
do
if [ -f "$i" ]; then
sed -n "/$PAT/p" $i
else
echo "ERROR: $i not a file." >&2
```

```
done
return 0
}
```

2. 以下命令可以完成此任务：

$ uptime | sed 's/.* load/'

3. 有两种可能的解决方案：

$ df -k | sed -n '/\/$/p'

$ df -k | sed '/^\/1/ d'

4. 以下命令将解决此问题：

/bin/ls -al | sed -e 's/^[^ ]*/-d' -e 's/*[0-9].* / /'

## 第17小时

1. 一种可能的实现如下：

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

2. 一种可能的解决方案是
