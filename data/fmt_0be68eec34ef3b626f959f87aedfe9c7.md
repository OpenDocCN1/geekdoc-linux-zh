
Ballroom Specialties:1221

Poolside Carts:1320

Formal Dining Specials:1340

Reservation Logs:1410

Plumbing Supplies:1423

Office Equipment:1361

Carpeting Services:1395

Auto Maintenance:1544

Pianos and Violins:1446

## 动手项目

```
mpmalmer@localhost:~ 
$ Edit View Tags Help
Lobby Furniture:1201
Ballroom Specialties:1221
Poolside Cards:1236
Formal Dining Specialties:1340
Reservation Logs:1410
mpmalmer@localhost:~ -cat product2
Plumbing Supplies:1422
Office Equipment:1361
Carpeting Services:1395
Auto Maintenance:1444
Pianos and Violins:1446
mpalmer@localhost:~ -cat product1 product2 product3
Lobby Furniture:1201
Ballroom Specialties:1221
Poolside Cards:1236
Formal Dining Specialties:1340
Reservation Logs:1410
Plumbing Supplies:1422
Office Equipment:1361
Carpeting Services:1395
Auto Maintenance:1444
Pianos and Violins:1446
mpalmer@localhost:~ -ls
```

图 4-11 使用 `cat` 命令创建并合并文件

## 项目 4-10

在项目 4-10 中，你学习了如何使用 `cat` 命令合并文件。在这个项目中，你使用另一种方法——`paste` 命令合并文件。在这里，你合并了在项目 4-10 中创建的两个 `product` 文件，以两个单独列显示这些文件中的记录。

使用 `paste` 命令合并文件：

1. 如果你直接从项目 4-10 继续，输入 `clear` 并按回车清除屏幕。

2. 输入 `paste product1 product2` 并按回车。

此命令行序列意味着“将名为 `product1` 的文件与 `product2` 文件合并，并在屏幕上使用每个文件内容的单独一列来显示结果”（见图 4-14）。列看起来不整齐，是因为文件中的记录长度不同，并且通过制表符分隔成列（你在屏幕上看不到制表符）。

3. 在此示例中，你如何将 `paste` 命令的输出写入文件而不是屏幕？

![](img/0a988e998d76ede7c21a57edbc89e490_215_0.png)

# 196 第 4 章 UNIX/Linux 文件处理

```
palmer@localhost:~# [x]
mpmer@localhost:-$ -is paste product12
Lobby Furniture:1201 Plumbing Supplies:1422
Bedroom Specials:1321 Officer Element:1361
Poolside Carts:1320 Carpeting Services:1395
Formal Dining Specials:1340 Auto Maintenance:1544
Reservation Logs:1410 Planus and Victims:1416
palmer@localhost:-$
```

```

图 4-14 使用 `paste` 命令合并文件

## 项目 4-12

`cut` 命令在处理和展示基本数据文件内容方面具有多功能性。在这个项目中，你首先开始创建两个文件：`corp_phones1` 和 `corp_phones2`。`corp_phones1` 包含五条变长度的记录，并用冒号（:）分隔记录中的每个字段。本章之前所示的图 4–2(c) 阐释了这种文件结构。`corp_phones2` 也包含了固定长度的记录，如图 4–2(b) 所示。图 4-15 展示了这两个文件的内容。你可以使用 `cut` 命令处理任一文件来提取姓名列表。

创建 `corp_phones1` 和 `corp_phones2` 文件：

- 1. 使用 `vi` 或 `Em` 编辑器创建 `corp_phones1` 文件。
- 2. 按照所示的内容准确输入以下行文本。在每行末尾按回车：
`219:432:4567:Harrison:Joel;M:4540:Accountant:09-12-1985`
`219:432:4587:Mitchell:Barbara;C:4541:Admin Asst:12-14-1995`
`219:432:4589:Olson:Timothy;H:4544:Supervisor:06-30-1983`
`219:432:4591:Moore:Sarah;H:4500:Dept Manager:08-01-1978`
`219:432:4527:Polk:John;S:4520:Accountant:09-22-1998`
- 3. 保存文件，并创建一个名为 `corp_phones2` 的新文件。
- 4. 按照所示的内容准确输入以下行文本。参考图 4-15 获取每个字符的精确位置。在每行末尾按回车。在这个文件中，你正在创建固定长度的记录，这意味着每个字段必须从特定的列开始，并且彼此对齐。例如，电话区号

## 动手项目 197

```

文件名: corp_phones1 (变长度记录 - 字段由冒号 : 分隔)

219:432:4567:Mitchell:Joel:4540:Olson:Barbara:C:4541:Admin Asst:09-12-1985

219:432:4567:Mitchell:Barbara:C:4541:Admin Asst:12-14-1995

219:432:4589:Olson:Timothy:H:4544:Supervisor:06-30-1983

219:432:4591:Moore:Sarah:H:4500:Dept Manager:08-01-1978

219:432:4527:Polk:John:S:4520:Accountant:09-22-1998

存储空间 = 279 字节

```

```

文件名: corp_phones2 (固定长度记录)

| 字符位置 | 1-3 | 7 | 9-12 | 14-25 | 26-35 | 36-41 | 43-58 | 59-68 |

| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |

| 219 | 432 | 4567 | Harrison | Joel | M | 4540 | Accountant | 09-12-1985 |

| 219 | 432 | 4587 | Mitchell | Barbara | C | 4541 | Admin Asst | 12-14-1995 |

| 219 | 432 | 4589 | Olson | Timothy | H | 4544 | Supervisor | 06-30-1983 |

| 219 | 432 | 4591 | Moore | Sarah | H | 4500 | Dept Manager | 08-01-1978 |

| 219 | 432 | 4527 | Polk | John | S | 4520 | Accountant | 09-22-1998 |

存储空间 = 345 字节

```

图-15 公司示例电话文件结构的两个版本

219 位于第 1 到 3 列。姓名从第 14 列开始，可以延伸到第 25 列。

```

219 432 4567 Harrison      Joel      M 4540 Accountant      09-12-1985

219 432 4587 Mitchell    Barbara  C 4541 Admin Asst      12-14-1995

219 432 4589 Olson       Timothy  H 4544 Supervisor      06-30-1983

219 432 4591 Moore       Sarah    H 4500 Dept Manager   08-01-1978

219 432 4527 Polk         John      S 4520 Accountant      09-22-1998
```
