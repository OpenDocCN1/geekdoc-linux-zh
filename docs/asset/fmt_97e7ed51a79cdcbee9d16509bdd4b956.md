
```bash
read _ANS
: ${_ANS=$_DEFAULT}
if [ "$ANS" = "" ]; then
  case $ANS in
    Y) return 0 ;;
    N) return 1 ;;
  esac
fi
case $ANS in
  y|Y|Yes|YES
  return 0
  ;;
  n|N|No|NO
  return 1
  ;;
  *) echo "Answer either Y or N, default is $_DEFAULT"
  ;;
esac
done
}
```

```bash
display_rec()
{
# display_rec
# could use cat << here document
tput cup 5 3
echo "EMPLOYEE NO: $CODE"
echo "FIRST NAME : $F_NAME"
echo "SURNAME : $S_NAME"
echo "DEPARTMENT : $DEPART"
echo -e "\n\n"
}
```

```bash
no_recs()
{
# no_recs
echo -e "\n\nSorry could not find a record with the name $STR"
}
```

```bash
get_rec()
{
# get_rec
clear
echo -n "Enter the employee surname : "
read STR
if [ "$STR" = "q" ]; then
  return 1
fi
```

```bash
REC=0
MATCH=no
```

```bash
if [ "$STR" != "" ]; then
  while read CODE F_NAME S_NAME DEPART
  do
    REC=$(expr $REC + 1)
    tput cup 3 4
    echo -n " searching record.. $REC"
    if [ "$S_NAME" = "$STR" ]; then
      MATCH=yes
      display_rec
      break
    else
      continue
    fi
  done $DBFILE
else
  echo "Enter a surname to search for or q to quit"
  if [ "$MATCH" = "no" ]; then
    no_recs
  fi
fi
```

```bash
SAVEDIFS=$IFS
IFS=
get_rec
if [ "$MATCH" = "yes" ]; then
  if continue_promptYN "Do You Wish To DELETE This Record " "N"; then
    echo "DEL"
    grep -v $STR DBFILE >HOLD1 2>/dev/null
    if [ $? -ne 0 ]; then
      echo "Problems creating temp file $HOLD1..check it out"
      exit 1
    fi
    mv $HOLD1 DBFILE
    if [ $? -ne 0 ]; then
      echo "Problems moving temp file..check it out"
      exit 1
    fi
    # sort the file after changes
    sort +2 -t: $DBFILE >HOLD2 2>/dev/null
    if [ $? -ne 0 ]; then
      echo "problems trying to sort the file..check it out"
      exit 1
    fi
    mv $HOLD2 $DBFILE
    if [ $? -ne 0 ]; then
      echo "problems moving the temp sort file..check it out"
      exit 1
    fi
  else
    echo "no deletion"
    # no deletion
  fi # if wish to delete
fi # if match
# restore IFS settings
IFS=$SAVEDIFS
```

# 374 创建屏幕输入

## 22.3 修改记录

我们已经看到了修改记录的大部分代码。我们在查看删除记录时已经见过这些代码。

当找到正确的记录后，我们简单地将所有记录字段变量赋值给一个临时变量，使用默认赋值变量：

`: {default_variable:=variable}`

用户只需在他们不想更改的字段上按回车键即可。默认值将替换临时变量。只需通过在相邻字段中输入新值，即可进行任何修改。

```bash
echo -n -e "EMPLOYEE NO: $CODE\n"
```

```bash
echo -n "FIRST NAME : [$F_NAME] >"
read F_NAME
: {_F_NAME:=$F_NAME}
```

文件的实际更新再次使用 `grep` 配合 `-v` 选项完成。除了正在修改的记录外，所有记录都会被重定向到一个临时文件。使用员工编号作为 `grep` 字符串：

```bash
grep -v $CODE $DBFILE >HOLD1
```

询问用户是否想要保存此条记录。如果回答是是，则新更新的记录也会追加到临时文件中。最后，将临时文件移动到原始文件 `DBFILE`。

```bash
echo "$CODE:$F_NAME:$S_NAME:$S_DEPART" >>HOLD1
mv $HOLD1 $DBFILE
```

然后对文件进行排序，输出重定向到临时文件，然后移回原始文件 `DBFILE`。对文件移动进行最后的状态测试，如果有任何问题将通知用户。在实际运行的脚本中，我们在添加记录时执行的验证测试也将在此处进行。以下是修改记录时的输出样式。

输入员工姓氏：Penny

查找记录.. 7

```
EMPLOYEE NO: 98211
FIRST NAME : Simon
SURNAME : Penny
DEPARTMENT : Services
```

这是您想要修改的记录吗 [Y..N] [Y]: amending

EMPLOYEE NO: 98211

FIRST NAME : Simon

SURNAME : Penny

DEPARTMENT : Services

准备好保存此记录 [Y..N] [Y]:

这里是修改记录的完整脚本：

```bash
#!/bin/sh
# databasechange
# amend a record

# ignore signals
trap "" 15

# temp files
HOLD1=.$$
HOLD2=.$$

continue_promptYN()
{
# continue_prompt
_STR=$1
_DEFAULT=$2
# check we have the right params
if [ $# -lt 1 ]; then
echo "continue_prompt: I need a string to display"
return 1
fi
while
do
  echo -n "$_STR [Y..N] [$_DEFAULT]:"
  read ANS
  : ${_ANS=$_DEFAULT}
  if [ "$ANS" = "" ]; then
    case $ANS in
      Y) return 0 ;;
      N) return 1 ;;
    esac
  fi
  case $ANS in
    y|Y|Yes|YES
      return 0
      ;;
    n|N|No|NO
      return 1
      ;;
    *) echo "Answer either Y or N, default is $_DEFAULT"
      ;;
  esac
done
}

display_rec()
{
# display_rec
# could use cat << here document
tput cup 5 3
echo "EMPLOYEE NO: $CODE"
echo "FIRST NAME : $F_NAME"
echo "SURNAME : $S_NAME"
echo "DEPARTMENT : $DEPART"
echo -e "\n\n"
}

no_recs()
{
# no_recs
echo -e "\n\nSorry could not find a record with the name $STR"
}

get_rec()
{
# get_rec
clear
echo -n "Enter the employee surname : "
read STR
if [ "$STR" = "q" ]; then
  return 1
fi
}
```

```bash
REC=0
MATCH=no

if [ "$STR" != "" ]; then
  while read CODE F_NAME S_NAME DEPART
  do
    REC=$(expr $REC + 1)
    tput cup 3 4
    echo -n " searching record.. $REC"
    if [ "$S_NAME" = "$STR" ]; then
      MATCH=yes
      display_rec
      break
    else
      continue
    fi
  done $DBFILE
else
  echo "Enter a surname to search for or q to quit"
  if [ "$MATCH" = "no" ]; then
    no_recs
  fi
fi
```

```bash
SAVEDIFS=$IFS
IFS=
get_rec
if [ "$MATCH" = "yes" ]; then
  if continue_promptYN "Do You Wish To DELETE This Record " "N"; then
    echo "DEL"
    grep -v $STR DBFILE >HOLD1 2>/dev/null
    if [ $? -ne 0 ]; then
      echo "Problems creating temp file $HOLD1..check it out"
      exit 1
    fi
    mv $HOLD1 DBFILE
    if [ $? -ne 0 ]; then
      echo "Problems moving temp file..check it out"
      exit 1
    fi
    # sort the file after changes
    sort +2 -t: $DBFILE >HOLD2 2>/dev/null
    if [ $? -ne 0 ]; then
      echo "problems trying to sort the file..check it out"
      exit 1
    fi
    mv $HOLD2 $DBFILE
    if [ $? -ne 0 ]; then
      echo "problems moving the temp sort file..check it out"
      exit 1
    fi
  else
    echo "no deletion"
    # no deletion
  fi # if wish to delete
fi # if match
# restore IFS settings
IFS=$SAVEDIFS
```

## 22.4 查看记录

用户可以查看所有记录或只查看特定记录。如果用户想查看所有记录，简单的 `cat` 和 `awk` 语句即可实现。如果记录包含许多字段，则需要更友好的输出，但这足以满足我们的需求。

```bash
if [ "$STR" = "all" ]; then
  echo "Surname Name Employee Code"
  echo ""
  cat $DBFILE|awk -F: '{print $2"\t"$3"\t"$1"}' | more
  return 0
fi
```

显示单条记录的代码已经在删除和修改部分涵盖过了。一个细小的变化是当用户选择此选项时，可以打印记录。这里是发送记录到打印机的代码段：

```
pr << MAYDAY
RECORD No : $REC
EMPLOYEE NUMBER : $CODE
EMPLOYEE NAME : $F_NAME
EMPLOYEE SURNAME : $S_NAME
EMPLOYEE DEPARTMENT : $DEPART
MAYDAY
```

以下是查看记录时的输出样式：

输入员工姓氏以查看或输入 all 查看所有记录：Wilson

查找记录.. 8

```
EMPLOYEE NO: 89232
FIRST NAME : Peter
SURNAME : Wilson
DEPARTMENT : IT
```

要打印此记录吗 [Y..N] [N]:

这里是查看记录的完整脚本：

```bash
$ pg databaseview
#!/bin/sh
# dbaseview
# view records
```

# 380 创建屏幕输入
