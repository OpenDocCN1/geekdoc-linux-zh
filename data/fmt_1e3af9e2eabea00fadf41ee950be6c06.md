
#### OR 运算符 (`||`)

`OR` 运算符只要它连接的条件中至少有一个为真，就返回真。在 shell 脚本中，它用双竖线 `||` 表示。当多种条件可以触发同一组命令时，该运算符非常有用。

```bash
if [ $a -gt 5 ] || [ $b -lt 10 ]; then
  echo "At least one condition is true"
else
  echo "Both conditions are false."
fi
```

示例脚本评估变量 `$a` 是否大于 `5` 或者 `$b` 是否小于 `10`。将显示消息“At least one condition is true”。

#### NOT 运算符 (`!`)

`NOT` 运算符是一个一元运算符，用于反转条件的布尔值。在 shell 脚本中，它用感叹号 `!` 表示。

```bash
if ! [ $a -gt 5 ]; then
  echo "$a is not greater than 5"
else
  echo "$a is greater than 5"
fi
```

## 4.10 # 用于菜单的 `select` 循环

`select` 循环是 `bash` 中的一个强大功能，便于创建交互式菜单。该循环特别适用于展示一组备选列表。其语法为：

```bash
select var in list
do
  commands
done
```

在这里，`var` 是用于存储用户选择的变量，`list` 代表一个用空格分隔的可选项目列表。在用户做出选择后，将执行 `commands` 块。

### 示例：基础菜单

为了说明 `select` 循环的基本用法，请考虑以下脚本，它提示用户选择一种水果：

```bash
#!/bin/bash
PS3="Please select "
select fruit in Apple Banana Orange Quit
do
  case $fruit in
    Apple)
      echo "You selected Apple."
      ;;
    Banana)
      echo "You selected Banana."
      ;;
    Orange)
      echo "You selected Orange."
      ;;
    Quit)
      echo "Exiting"
      break
      ;;
    *)
      echo "Invalid option. Please try again."
      ;;
  esac
done
```

# 解释：

`PS3` 是在用户输入前显示的提示字符串。

`select fruit in Apple Banana Orange` 是呈现给用户的列表。

`case $fruit` 评估用户的选择并执行相应的命令。

输出：

1) Apple 2) Banana 3) Orange 4) Quit Please select fruit:

用户随后可以输入与其选择相对应的数字。如果用户选择 `4`，脚本将终止。

### 处理无效输入

`select` 循环允许轻松管理无效输入。如果用户输入了无效数字（例如上面示例中的 `5`），脚本将重新显示菜单并提示用户重试。这种行为由 `case` 语句的块管理，该块作为意外输入的默认情况处理。

`select` 循环允许定制化并具备了额外功能：

默认：如果用户在没有输入数字的情况下按回车键，提示将重新出现。可以通过检查 `$REPLY` 是否为空并进行相应的处理来控制这一点。

动态：列表可以动态生成，允许脚本能够灵活地响应变化的输入数据。

示例：动态菜单

考虑一个从数组动态生成菜单的脚本：

```bash
#!/bin/bash

options=("Add User" "Delete User" "Quit")
PS3="Please select an option: "
select opt in "${options[@]}"; do
  case $opt in
    "Add User")
      echo "Adding a new user."
      ;;
    "Delete User")
      echo "Deleting a user."
      ;;
    "Quit")
      echo "Exiting"
      break
      ;;
    *)
      echo "Invalid option."
      ;;
  esac
done

# 解释：

options=("Add User" "Delete User") - 一个存放菜单项的数组。
select opt in "${options[@]}" - select 循环遍历数组。

动态列表生成在与其它系统组件集成的脚本中特别有用，能够对展示的选项进行实时更新。

### 实际应用

`select` 循环的用途不仅限于简单的菜单。它可以集成到更大的脚本中，用于：

系统管理：在自动化设置或维护脚本期间促进用户交互。

配置：通过交互方式引导用户完成软件配置步骤。

教育：创建交互式教程或测验。

### 最佳实践

在使用 `select` 循环时：

- 确保提示信息具有信息性，并清晰地设定用户预期。
- 始终包含一个机制（例如“退出”选项）让用户能够退出循环。
- 验证用户输入，以优雅的方式处理意外的选择。

通过采用这些实践，`select` 循环可以成为增强 shell 脚本用户友好界面的健壮工具，最大限度地减少捕获和处理用户输入的复杂性。

# 4.11

# 控制结构的实际示例

为了巩固对控制结构的理解，探索整合了各种类型控制语句的实际示例至关重要。这些示例演示了如何结合条件语句、循环和逻辑运算符来高效地解决现实世界的问题。

考虑处理文件名列表并根据其扩展名执行不同操作的任务。这需要使用条件语句（`if`, `elif`, `else`）、`case` 语句和循环。以下示例脚本将扫描目录并根据文件类型应用特定的命令。

```bash
#!/bin/bash

# 包含要处理文件的目录

DIRECTORY="/path/to/directory"

# 如果不存在则为每个扩展名创建目录

mkdir -p "$DIRECTORY/images"

mkdir -p "$DIRECTORY/documents"

mkdir -p "$DIRECTORY/archives"

mkdir -p "$DIRECTORY/others"

# 遍历目录中的每个文件

for FILE in "$DIRECTORY"/*; do

  # 提取文件扩展名

  EXTENSION="${FILE##*.}"

  # 根据扩展名执行操作

  case "$EXTENSION" in

    jpg | png | gif)

      mv "$FILE" "$DIRECTORY/images/"

      ;;

    pdf | doc | txt)

      mv "$FILE" "$DIRECTORY/documents/"

      ;;

    zip)

      mv "$FILE" "$DIRECTORY/archives/"

      ;;

    *)

      mv "$FILE" "$DIRECTORY/others/"

      ;;

  esac

done
```

该脚本利用 `for` 循环遍历指定目录中的所有文件。然后使用 `case` 语句检查文件扩展，并根据扩展名将每个文件移动到相应的子目录。

另一个常见场景是在循环中读取用户输入并根据该输入执行操作。考虑一个简单的计算器脚本示例，它反复提示用户输入两个数字和一个运算符，直到用户决定退出。

```bash
#!/bin/bash

# 执行算术运算的函数

calculate() {

  local NUM1=$1

  local NUM2=$2

  local OPERATOR=$3

  case "$OPERATOR" in

    +)

      echo "$(( NUM1 + NUM2 ))"

      ;;

    -)

      echo "$(( NUM1 - NUM2 ))"

      ;;

    *)

      echo "$(( NUM1 * NUM2 ))"

      ;;

    /)

      if [ "$NUM2" -ne 0 ]; then

        echo "$(( NUM1 / NUM2 ))"

      else

        echo "Error: Division by zero"

      fi

      ;;

    *)

      echo "Invalid operator"

      ;;

  esac

}

while true; do

  read -p "Enter first number: " NUM1
```
