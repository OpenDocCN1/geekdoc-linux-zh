
```
mysql> SELECT phrase, MATCH(phrase) AGAINST('time') AS relevance
       -> FROM apothegm;

+---------------------+-------------------------------------+-------------+
| phrase              |                                     | relevance   |
+---------------------+-------------------------------------+-------------+
| Time as he grows old teaches many lessons         | 1.3253291845322 |
| Mr. Watson, come here. I want you!                | 0             |
| It is hard for an empty bag to stand upright      | 0             |
| Little strokes fell great oaks                    | 0             |
| Remember that time is money                       | 1.3400621414185 |
| Bell, book, and candle                            | 0             |
| A soft answer turneth away wrath                  | 0             |
| Speak softly and carry a big stick                | 0             |
| But, soft! what light through yonder window breaks? | 0             |
| I light my candle from their torches               | 0             |
+---------------------+-------------------------------------+-------------+
```

自然语言搜索会找到包含任意搜索词的行，因此像下面的查询会返回包含“hard”或“soft”的行：

```
mysql> SELECT * FROM apothegm WHERE MATCH(phrase)
       -> AGAINST('hard soft');
```

+---------------------+-------------------------------------+
| attribution         | phrase                              |
+---------------------+-------------------------------------+
| Benjamin Franklin   | It is hard for an empty bag to stand upright   |
| Proverbs 15:1       | A soft answer turneth away wrath   |
| William Shakespeare | But, soft! what light through yonder window breaks? |
+---------------------+-------------------------------------+

自然语言模式是默认的全文搜索模式。在 MySQL 5.1 及以上版本中，通过在搜索字符串后添加 `IN NATURAL LANGUAGE MODE` 可以明确指定此模式。以下语句执行与前面示例相同的搜索：

```
SELECT * FROM apothegm WHERE MATCH(phrase)
AGAINST('hard soft' IN NATURAL LANGUAGE MODE);
```

### 2.15.2 布尔模式 FULLTEXT 搜索

通过使用布尔模式 FULLTEXT 搜索，可以获得对多词匹配的更大控制权。这种搜索通过在 `AGAINST()` 函数中的搜索字符串后添加 `IN BOOLEAN MODE` 来执行。布尔搜索具有以下特征：

- 忽略 50% 规则；即使词出现在超过半数的行中，搜索也能找到这些词。
- 结果不按相关性排序。
- 可以执行短语搜索，要求所有词以特定顺序出现。要匹配短语，请用双引号指定短语中的词。匹配发生在包含相同词且顺序与短语中列出的顺序相同的行中：

```mysql
mysql> SELECT * FROM apothem
    -> WHERE MATCH(attribute, phrase)
    -> AGAINST("bell book and candle" IN BOOLEAN MODE);
```

| attribute | phrase |
|---|---|
| Miguel de Cervantes | Bell, book, and candle |

- 可以对不是 FULLTEXT 索引一部分的列执行布尔模式全文搜索，尽管这比使用索引列要慢得多。

对于布尔搜索，可以在搜索字符串中的词上应用修饰符。前导加号或减号要求匹配行中存在或不存在某个词。例如，搜索字符串 `'bell'` 匹配包含“bell”的行，但在布尔模式下，搜索字符串 `'+bell -candle'` 仅匹配包含“bell”且不包含“candle”的行。

```mysql
mysql> SELECT * FROM apothem
    -> WHERE MATCH(attribute, phrase)
    -> AGAINST('bell');
```

| attribute | phrase |
|---|---|
| Alexander Graham Bell | Mr. Watson, come here. I want you! |
| Miguel de Cervantes | Bell, book, and candle |

```mysql
mysql> SELECT * FROM apothem
    -> WHERE MATCH(attribute, phrase)
    -> AGAINST('+bell -candle' IN BOOLEAN MODE);
```

| attribute | phrase |
|---|---|
| Alexander Graham Bell | Mr. Watson, come here. I want you! |

## 2.15 使用全文检索

尾部的星号作为通配符，使得任何包含以搜索词开头的单词的行都会匹配。例如，`*soft*` 匹配“soft”、“softly”、“softness”等：

```sql
mysql> SELECT * FROM apothegm WHERE MATCH(phrase)
    -> AGAINST(`*soft*` IN BOOLEAN MODE);
```

| 出处 | 短语 |

|---|---|

| 箴言 15:1 | 柔和的回答息怒止暴 |

| 威廉·莎士比亚 | 可是，轻声问，那边窗子透进来的是什么光？ |

| 西奥多·罗斯福 | 口齿温和，手持大棒 |

但是，通配符功能不能用于匹配短于最小索引词长的单词。

附录 C“运算符和函数参考”中关于 `MATCH` 的条目列出了布尔模式修饰符的完整集合。

停用词在自然语言搜索中会被忽略，即使它们被标记为必需的也是如此。搜索 `+Alexander +the +great` 会找到包含“Alexander”和“great”的行，但会忽略停用词“the”。

### 2.15.3 带查询扩展的全文检索

带查询扩展的全文搜索执行两阶段搜索。初始搜索类似于常规的自然语言搜索。然后，此搜索中相关性最高的行用于第二阶段。这些行中的单词将与原始搜索词一起用于执行第二次搜索。由于搜索词集合更大，结果通常包含第一阶段未找到但与它们相关的行。

要执行这种搜索，请在搜索词后添加 `WITH QUERY EXPANSION`。以下示例提供了说明。第一个查询显示自然语言搜索。第二个查询显示查询扩展搜索。其结果包含一个不包含任何原始搜索词的额外行。找到该行是因为它包含单词“candle”，而该单词存在于自然语言搜索找到的某一行中。

```sql
mysql> SELECT * FROM apothegm
    -> WHERE MATCH(attribution, phrase)
    -> AGAINST(`bell book`);
```

| 出处 | 短语 |

|---|---|

| 米格尔·德·塞万提斯 | 铃、书，以及蜡烛 |
