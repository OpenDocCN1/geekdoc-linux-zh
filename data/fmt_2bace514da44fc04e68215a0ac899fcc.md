
```php
function display_entry($dbh)
{
    # Get script parameters; trim whitespace from the ID, but not
    # from the password, because the password must match exactly.
    $member_id = trim(script_param("member_id"));
    $password = script_param("password");

    if (empty($member_id))
        die("No member ID was specified\n");
    if (!ctype_digit($member_id))    # must look like integer
        die("Invalid member ID was specified (must be an integer)\n");
    if (empty($password))
        die("No password was specified\n");
    if (check_pass($dbh, $member_id, $password)) # regular member
        $admin = FALSE;
    else if (check_pass($dbh, 0, $password))    # administrator
        $admin = TRUE;
    else
        die("Invalid password\n");

    $stmt = "SELECT
                last_name, first_name, suffix, email, street, city,
                state, zip, phone, interests, member_id, expiration
                FROM member WHERE member_id = ?
                ORDER BY last_name";
    $sth = $dbh->prepare($stmt);
    $sth->execute(array($member_id));

    if (!($row = $sth->fetch()))
        die("No user with member_id = $member_id was found\n");

    printf("<form method=\"post\" action=\"%s?action=&id\">\n",
           script_name(),
           UPDATE_ENTRY);

    # Add member ID and password as hidden values so that next invocation
    # of script can tell which record the form corresponds to and so that
    # the user need not re-enter the password.

    hidden_field("member_id", $member_id);
    hidden_field("password", $password);

    # Format results of statement for editing

    print("<table>\n");
}
```

### 将成员 ID 显示为静态文本

```php
display_column ("Member ID", $row, "member_id", FALSE);

# $admin 在用户提供了管理员密码时为 true，
# 否则为 false。管理员用户可以修改过期日期，
# 普通用户则不能。

display_column ("Expiration", $row, "expiration", $admin);

# 将其他值显示为可编辑文本

display_column ("Last name", $row, "last_name");
display_column ("First name", $row, "first_name");
display_column ("Suffix", $row, "suffix");
display_column ("Email", $row, "email");
display_column ("Street", $row, "street");
display_column ("City", $row, "city");
display_column ("State", $row, "state");
display_column ("Zip", $row, "zip");
display_column ("Phone", $row, "phone");
display_column ("Interests", $row, "interests");

print ("</table>\n");

submit_button ("button", "Submit");
print  "</form>\n";

}
```

`display_entry()` 做的第一件事就是验证密码。如果用户提供的密码与 `member_pass` 表中存储的对应成员 ID 的密码匹配，或者与管理员密码（即特殊成员 ID `0` 的密码）匹配，`edit_member.php` 将以表单形式显示该条目，以便编辑其内容。密码检查函数 `check_pass()` 执行一个简单的查询，从 `member_pass` 表中获取一行数据，并将其密码列的值与用户在登录表单中提供的密码进行比较：

```php
function check_pass ($dbh, $id, $pass)
{
  $stmt = "SELECT password FROM member_pass WHERE member_id = ?";
  $sth = $dbh->prepare ($stmt);
  $sth->execute (array ($id));
  # 如果找到密码且匹配则为 TRUE
  return (($row = $sth->fetch ()) && $row ["password"] == $pass);
}
```

假设密码匹配，`*display_entry()*` 会从成员表中查找与给定成员 ID 对应的行，然后继续生成一个初始化了该行值的编辑表单。大多数字段都被呈现为可编辑文本字段，以便用户可以更改它们，但有两个例外。首先，`member_id` 值被显示为静态文本。这是唯一标识该行的键值，因此不应被更改。其次，过期日期不是我们希望联盟会员能够更改的内容。（他们能够将日期推迟到更远的未来，实际上是在未支付会费的情况下更新他们的会员资格。）另一方面，如果在登录时提供了管理员密码，脚本确实以可编辑字段的形式呈现过期日期。假设联盟秘书知道这个密码，这使秘书能够更新续会成员的过期日期。

`*display_column()*` 函数处理字段标签和值的显示。其参数包括：显示在字段值旁边的标签、包含要编辑的行的数组、包含字段值的行内列名，以及一个布尔值，指示以可编辑还是静态形式显示该值。最后一个值是可选的，默认值为 TRUE：

```php
function display_column ($label, $row, $col_name, $editable = TRUE)
{
    print ("<tr>\n");
    print ("<td>" . htmlspecialchars($label) . "</td>\n");
    print ("<td>");
    if ($editable) # 显示为可编辑字段
        text_field ("row[$col_name]", $row[$col_name], 80);
    else              # 显示为只读文本
        print (htmlspecialchars ($row[$col_name]));
    print ("</td>\n");
    print ("</tr>\n");
}
```

对于可编辑值，`*display_column()*` 生成具有 `row[col_name]` 格式的文本字段。这样，当用户提交表单时，PHP 会将所有字段值放入一个数组变量中，元素以列名为键。这使得提取表单内容并将在更新数据库行时将每个字段值与其对应的成员表列相关联变得容易。例如，通过获取数组到 `$row` 变量中，我们可以使用 `$row['phone']` 访问电话号码。
