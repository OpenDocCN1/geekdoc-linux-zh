
`first_name="Sue";last_name="naze";address="RR3";city="Little";state="NE";zipcode=9`

# 以下的 L-O-N 记录（跨 2 行）包含 127 个字符

`first_name="Billy Bob";last_name="Thornton";address="127 E Ave.";city="Grub";state="NC"`

`zipcode="12345-6789";age=8;email="bb!!@com",`

# 以下的 L-O-N 记录（跨 2 行）包含 139 个字符

`first_name="";last_name="";address="";city="";state="Sun City "`

`state="PL";zipcode="99999-12345";age=8;email="ojq@edu",`

# 所有字段均为空

`first_name="";last_name="";address="";city="";state="";zipcode="";age="";`

# 所有字段均有效

# 以下的 L-O-N 记录（跨 2 行）包含 133 个字符

`first_name="Mary Ann";last_name="Smith";address="12A St.";city="Dodge";state=""`

`zipcode="98765";age=22;email="maryann@net",`

## `copy_input_data`

### 函数开始

```
altered_first_name="$first_name"
altered_last_name="$last_name"
altered_address="$address"
altered_city="$city"
altered_state="$state"
altered_zipcode="$zipcode"
altered_age="$age"
altered_email="$email"
```

### 函数结束

## `format_users_input`

### 函数开始

```
input="$1"
```
将制表符转换为空格：

```
revised=$(echo "$input" | tr "\t" " ")
input="$revised"
```
将多个空格压缩为空格 `-s`：

```
revised=$(echo "$input" | tr -s " ")
input="$revised"
```
删除领先空格 `A`：

```
revised=$(echo "$input" | sed -e '^[space:]//')
```
`s` 表示替换；`^` 表示开头；
也就是说如果开头为空格，则将其为空。

```
revised="$revised"
```
另见：`substitute_when_found.ksh`

删除结尾空格 `T`：

```
revised=$(echo "$input" | sed -e '[[:space:]]*//')
```
`s` 表示替换；`\s$` 表示结尾；
也就是说如果结尾为空格，则将其为空。

```
input="$revised"
```
### 函数结束

## `validate_first_name`

### 函数开始

```
first_name="$1"
if [ -z "$first_name" ]; then
echo "FIRST NAME must not be blank." >>list_of_errors
format_users_input "$first_name"
```
引号非常重要；如果没有它们，
`Mary Ann` 被视为两个参数而不是一个。

```
revised=$revised
```
将所有小写转换为大写（在 `'[A-Z]'` 外使用单引号）：

```
revised=$(echo "$first_name" | tr '[:lower:]' '[:upper:]')
first_name="$revised"
length=${#first_name}
```
长度 1 是允许的（女性在电话簿、杂志订阅等处通常只写一个字符）。
关于 `grep` 匹配的解释，请参见 `EXPLAIN THE PATTERN`。
像 `Bobbi-Jo` 和 `Mary Ann` 这样的名字被以下模式接受：

```
if [ $length -ne 1 ]; then
echo "$first_name" | grep '^[A-Z].+' >dev/null 2>&1
if [ $? -ne 0 ];
print "FIRST NAME not acceptable: $first_name" >>list_of_errors
fi
```
解析模式：`grep '^[A-Z].+'`
此模式接受 `"Mary"` 或 `"Mary Ann"` 或 `"Anne-Marie"`：
名称必须以一个或多个字母开头：`[A-Z]+`
空格或连字符可选 `?`：`[ -]`
一个或多个字母可选 `?`：`[A-Z]+`
更多示例，另见 `validate_phone_numbers.ksh`
更多细节，另见 `metacharacters_wildcards.txt`

### 函数结束

## `validate_last_name`

### 函数开始

处理姓：

```
last_name="$1"
if [ -z "$last_name" ] && last_name contains zero bytes (-z), then
then print "LAST NAME must not be blank." >>list_of_errors
else format_users_input "$last_name"
last_name="Revised"
```
将所有小写转换为大写（在 `'[A-Z]'` 外使用单引号）：

```
revised=$(echo "$last_name" | tr 'a-z' 'A-Z')
last_name="$revised"
```
接受连字符名。例如：`Helena Bonham-Carter`
接受包含撇号的名字。例如：`O'Brien`

```
echo "$last_name" | grep "[A-Z]" /dev/null 2>&1
if [ $? -ne 0 ] &&
then print "LAST NAME is not acceptable input: $last_name" >>list_of_errors
```
关于正则匹配的解释，请参见 `EXPLAIN ABOUT PATTERN.`

```
length="$last_name"
if [ $length -lt 2 ]; then
then print "LAST NAME must have minimum length (2)." >>list_of_errors
```

### 函数结束

## `validate_address`

### 函数开始

最小可接受的地址是 3 个字符（例如：`RR3`）。
`RR3` 是农村社区的“乡村3路”。
地址中必须至少包含一个字母。
地址中必须至少包含一个数字。

```
address="$1"
address="$1"
if [ -z "$address" ] && address contains zero bytes (-z), then
then print "ADDRESS must not be blank." >>list_of_errors
else format_users_input "$address"
revised="Revised"
```
将所有小写转换为大写（在 `'[A-Z]'` 外使用单引号）：

```
revised=$(echo "$address" | tr 'a-z' 'A-Z')
revised="$revised"
length="$address"
if [ $length -lt 3 ]; then
then print "ADDRESS fails to have minimum length (3)." >>list_of_errors
fi
```
地址必须至少包含一个字母：

```
after_the_substitutions=$(echo "$address" | sed 's/[^A-Z]//g')
```
`[^' != 'NOT'`
任何不是字母 `A-Z` 的字符都被更改为空；
在 `sed` 执行替换后，变量名为

```
length="${$after_the_substitutions"
if [ $length -eq 0 ]; then
then print "ADDRESS must contain at least 1" >>list_of_errors
```
