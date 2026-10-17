
NULL 安全相等；此运算符与 `=` 类似，但即使操作数为 NULL，当它们相等时也评估为 1。

```
1 <=> 1                 → 1
1 <=> 2                 → 0
NULL <=> NULL           → 1
NULL = NULL             → NULL
```

最后两个示例展示了 `<=>` 和 `=` 如何处理 NULL 比较的不同方式。

### `<>`, `!=`

如果操作数不相等，则求值为 1，否则为 0。

```
3, 4 != 3,4                    → 0
'abc' <> 'ABC'                 → 0
BINARY 'abc' <> 'ABC'          → 1
'abc' != 'def'                 → 1
```

### `<`

如果左操作数小于右操作数，则求值为 1，否则为 0。

```
3 < 10                     → 1
105.4 < 10e+1              → 0
'abc' < 'ABC'              → 0
'abc' < 'def'              → 1
```

### `<=`

如果左操作数小于或等于右操作数，则计算结果为 1；否则为 0。

```
'abc' <= 'a'                   → 0
'a' <= 'abc'                   → 1
13.5 <= 14                    → 1
(3 * 4) - (6 * 2) <= 0        → 1
```

### `>`

如果左操作数大于右操作数，则计算结果为 1；否则为 0。

```
PI() > 3                       → 1
'abc' > 'a'                   → 1
SIN(0) > COS(0)               → 0
```

### `>=`

如果左操作数大于或等于右操作数，则计算结果为 1；否则为 0。

```
'abc' >= 'a'                   → 1
'a' >= 'abc'                  → 0
13.5 >= 14                    → 0
(3 * 4) - (6 * 2) >= 0        → 1
```

### `expr BETWEEN min AND max`

`expr NOT BETWEEN min AND max`

如果 `expr` 位于 `min` 和 `max` 所跨度的值范围内（包含边界值），`BETWEEN` 的计算结果为 1；否则为 0。对于 `NOT BETWEEN`，则情况相反。如果操作数 `expr`、`min` 和 `max` 均为同类型，则这些表达式等价于：

```
expr BETWEEN min AND max
(min <= expr AND expr <= max)
```

如果操作数不是同类型，则会发生类型转换，且这两个表达式可能不再等价。`BETWEEN` 使用根据 `expr` 类型确定的比较规则进行评估：

- 如果 `expr` 是字符串，则操作数作为字符串按字典序进行比较，使用本节开头给出的规则。
- 如果 `expr` 是整数，则操作数作为整数按数值进行比较。
- 如果上述规则均不适用，则操作数作为浮点数按数值进行比较。

```
'def' BETWEEN 'abc' AND 'ghi'   → 1
'def' BETWEEN 'abc' AND 'def'   → 1
13.3 BETWEEN 10 AND 20         → 1
13.3 BETWEEN 10 AND 13        → 0
2 BETWEEN 2 AND 2             → 1
'B' BETWEEN 'A' AND 'a'       → 0
BINARY 'B' BETWEEN 'A' AND 'a' → 1
```

对于使用混合时间类型或混合时间类型与字符串的 `BETWEEN` 表达式，最好使用 `CAST()` 以确保所有操作数具有相同的类型。

### `CASE expr WHEN expr1 THEN result1 ... [ELSE default] END`

当存在初始表达式 `expr` 时，`CASE` 将其与每个 `WHEN` 后的表达式进行比较。对于第一个为真的匹配项，相应的 `THEN` 值即为结果。这用于将一个给定值与一组值进行比较时非常有用。

```
CASE 0 WHEN 'T' WHEN 0 THEN 'F' END        → 'F'
CASE 'F' WHEN 'T' THEN 1 WHEN 'F' THEN 0 END  → 0
```

当不存在初始表达式 `expr` 时，`CASE` 计算 `WHEN` 表达式。对于第一个为真（非零、非 `NULL`）的表达式，相应的 `THEN` 值即为结果。这对于执行非等值测试或测试任意条件非常有用。

```
CASE WHEN 1=0 THEN 'absurd' WHEN 1=1 THEN 'obvious' END → 'obvious'
```

如果没有 `WHEN` 表达式匹配，则 `ELSE` 值为结果。如果没有 `ELSE` 子句，`CASE` 计算结果为 `NULL`。

```
CASE WHEN 1 THEN 'true' ELSE 'false' END   → 'false'
CASE WHEN 1 THEN 'true' END                → NULL
CASE WHEN 1=0 THEN 'true' ELSE 'false' END  → 'false'
CASE WHEN 1/0 THEN 'true' END              → NULL
```

`CASE` 表达式的返回类型默认由返回值的聚合类型确定。

```
CASE 1 WHEN 0 THEN 0 ELSE 1 END      → 1
CASE 1 WHEN 0 THEN '0' ELSE '1' END   → '1'
```

然而，默认返回类型也受周围上下文的影响，这可能导致转换为字符串、数字等。

请注意，`CASE` 表达式与 E.2.1 节“控制结构语句”中描述的 `CASE` 语句不同。

### `expr IN (value1,value2 ,...)`

`expr NOT IN (value1,value2 ,...)`

如果 `expr` 是列表中的一个值，`IN()` 的计算结果为 1；否则为 0。对于 `NOT IN()`，则情况相反。以下表达式等价：

```
expr NOT IN (value1,value2,...)
NOT (expr IN (value1,value2,...))
```

如果列表中的所有值都是常量，`MySQL` 会对它们进行排序，并使用二分查找来评估 `IN()` 测试，这非常快速。

```
3 IN (1,2,3,4,5)									→ 1
'd' IN ('a','b','c','d','e')					→ 1
'E' IN ('a','b','c','d','e')					→ 0
3 NOT IN (1,2,3,4,5)							→ 0
'd' NOT IN ('a','b','c','d','e')			→ 0
'E' NOT IN ('a','b','c','d','e')			→ 1
```

### `expr IS (FALSE | TRUE | UNKNOWN)`

这些结构测试 `expr` 是否为逻辑假、真或未知，并返回 0（假）或 1（真）。值为 0 被视为假，非零、非 `NULL` 值被视为真，而 `NULL` 被视为未知。

```
2 IS FALSE								→ 0
2 IS TRUE								→ 1
2 IS UNKNOWN							→ 0
NULL IS FALSE							→ 0
NULL IS TRUE							→ 0
NULL IS UNKNOWN						→ 1
```

### `expr IS NULL`

`expr IS NOT NULL`

如果 `expr` 的值为 `NULL`，`IS NULL` 的计算结果为 1；否则为 0。`IS NOT NULL` 则相反。以下表达式等价：

```
expr IS NOT NULL
NOT (expr IS NULL)
```
