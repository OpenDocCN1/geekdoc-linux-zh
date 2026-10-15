
219 432 4527 Polk John S 4520 Accountant 09-22-1998

219 432 4591 Moore Sarah H 4500 Dept Manager 08-01-1978

219 432 4589 Olson Timothy H 4544 Supervisor 06-30-1983

### 2.
输入 `sort -t: +3 corp_phones1` 并按下回车键。这将按变长记录（`-t:`）排序，起始字段为姓氏（`+3`）。您将在屏幕上看到以下内容：

```
219:432:4567:Harrison:Joel:M:4540:Accountant:09-12-1985
219:432:4587:Mitchell:Barbara:C:4541:Admin Asst:12-14-1995
219:432:4591:Moore:Sarah:H:4500:Dept Manager:08-01-1978
219:432:4589:Olson:Timothy:H:4544:Supervisor:06-30-1983
219:432:4567:Polk:John:S:4520:Accountant:09-22-1998
```

### 3.
输入 `sort -t: +4 corp_phones1` 并按下回车键。这将按变长记录排序（`-t:` 表示字段由冒号分隔），起始字段为名字（`+4`）。您将在屏幕上看到以下内容：

```
219:432:4587:Mitchell:Barbara:C:4541:Admin Asst:12-14-1995
219:432:4567:Harrison:Joel:M:4540:Accountant:09-12-1985
219:432:4567:Polk:John:S:4520:Accountant:09-22-1998
219:432:4591:Moore:Sarah:H:4500:Dept Manager:08-01-1978
219:432:4589:Olson:Timothy:H:4544:Supervisor:06-30-1983
```

### 4.
若要按名字排序并创建输出文件 `Sorted_phones`，请输入 `sort -t: +4 -o sorted_phones corp_phones1` 并按下回车键。这将按名字对 `phones1` 文件进行排序，并创建一个输出文件 `sorted_phones`。

## 综合运用

现在，您可以一次性使用之前学过的众多文件处理工具。首先，使用 `cat` 命令创建 `vendors` 文件。供应商名称文件中的记录由两个以冒号分隔的字段组成：供应商编号和供应商名称。

要创建 `vendors` 文件：

1. 在 `$` 命令提示符后，输入 `cat>vendors` 并按下回车键。

2. 输入以下文本，每行末尾按下回车键：

   1201:Cromwell Interiors

   1221:Design Extras Inc.

   1320:Piedmont Plastics Inc.

   1340:Morgan Catering Service Ltd.

   1350:Pullman Elevators

   1360:Johnson Office Products

3. 按下 `Ctrl+D`。

图 4-4 展示了 Worldwide 可用于确定每个供应商提供何种产品的两个文件。

![](img/6d8286a85e2d8ad63e16f1801102da59_136_0.png)

在接下来的步骤中，使用 `cat` 命令创建 `products` 文件。`products` 文件中的记录由三个以冒号分隔的字段组成：产品编号、产品描述和供应商编号。

要创建 `products` 文件：

1. 在 `$` 命令提示符后，输入 `cat > products` 并按下回车键。

2. 输入以下文本，每行末尾按下回车键：

   S0107:Lobby Furniture:1201

   S0109:Ballroom Specialties:1221

   S0110:Poolside Carts:1320

   S0130:Formal Dining Specials:1340

   S0201:Reservation Logs:1410

3. 输入 `Ctrl+D` 结束 `cat` 命令

现在使用 `cut`、`paste` 和 `sort` 命令为 Worldwide Hotels 创建单一供应商报告。首先使用 `cut` 命令从 `products` 文件中提取产品描述和供应商编号，并将它们存储在 separate 文件 `p1` 和 `p2` 中。然后从 `vendors` 文件中提取供应商编号和名称，并将它们存储在 `v1` 和 `v2` 中。使用 `paste` 命令将两个供应商文件（`v1` 和 `v2`）合并到第三个文件 `v3` 中。然后将两个产品文件（`p1` 和 `p2`）合并到一个文件 `p3` 中。对 `v3` 和 `p3` 文件进行排序和合并，并将其输出发送到 `vrep` 文件，即供应商报告。

使用 `cut`、`paste` 和 `sort` 命令创建报告：

1. 在 `$` 命令提示符后，输入 `cut -f2 -d: products > p1` 并按下回车键。这意味着“从 `products` 文件中提取由冒号分隔的第二个字段的数据，并将其存储在 `p1` 文件中。”它将以下产品描述存储在 `p1` 文件中：

   - Lobby Furniture

   - Ballroom Specialties

   - Poolside Carts

   - Formal Dining Specials

   - Reservation Logs

2. 输入 `cut -f3 -d: products > p2` 并按下回车键。这意味着“从 `products` 文件中提取由冒号分隔的第三个字段的数据，并将其存储在 `p2` 文件中。”它将以下供应商编号存储在 `p2` 文件中：

   - 1201

   - 1221

   - 1320

   - 1340

   - 1410

3. 输入 `cut -f1 -d: vendors > v1` 并按下回车键。这意味着“从 `vendors` 文件中提取由冒号分隔的第一个字段的数据，并将其存储在 `v1` 文件中。”它将以下供应商编号存储在 `v1` 文件中：

   - 1201

   - 1221

   - 1320

   - 1340

   - 1350

   - 1360

4. 输入 `cut -f2 -d: vendors > v2` 并按下回车键。这意味着“从 `vendors` 文件中提取由冒号分隔的第二个字段的数据，并将其存储在 `v2` 文件中。”它将以下供应商名称存储在 `v2` 文件中：

   - Cromwell Interiors

   - Design Extras Inc.

   - Piedmont Plastics Inc.

   - Morgan Catering Service Ltd.

   - Pullman Elevators

   - Johnson Office Products

5. 输入 `paste v1 v2 > v3` 并按下回车键。这意味着“合并 `v1` 和 `v2` 中的数据，并将其定向到文件 `v3`。”它将以下供应商编号和产品描述存储在 `v3` 文件中：

   - 1201 Cromwell Interiors

   - 1221 Design Extras Inc.

   - 1320 Piedmont Plastics Inc.

   - 1340 Morgan Catering Service Ltd.

   - 1350 Pullman Elevators

   - 1360 Johnson Office Products

6. 输入 `paste p2 p1 > p3` 并按下回车键。这意味着“合并 `p2` 和 `p1` 中的数据，并将其定向到名为 `p3` 的文件。”它将以下供应商编号和产品描述存储在 `p3` 文件中：

   - 1201 Lobby Furniture

   - 1221 Ballroom Specialties

   - 1320 Poolside Carts

   - 1340 Formal Dining Specials

   - 1410 Reservation Logs

7. 输入 `sort -o vrep -m v3 p3` 并按下回车键。这意味着“合并 `v3` 和 `p3` 中的数据，并将输出定向到名为 `vrep` 的文件。”它将以下供应商编号和产品描述存储在 `vrep` 文件中：

   - 1201 Cromwell Interiors

   - 1201 Lobby Furniture

   - 1221 Ballroom Specialties

   - 1221 Design Extras Inc.

   - 1320 Piedmont Plastics Inc.

   - 1320 Poolside Carts

   - 1340 Formal Dining Specials

   - 1340 Morgan Catering Service Ltd.
