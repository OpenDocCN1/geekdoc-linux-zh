```
```code
(index_columns) [index_option] ...
| {FULLTEXT | SPATIAL} [INDEX | KEY]
    [index_name] (index_columns) [index_option] ...
| {CONSTRAINT [name] | FOREIGN KEY [fk_name]
    (index_columns) [reference_definition]
| CHECK (expr)
```
```

**col_definition:**

```
```code
data_type
[NOT NULL | NULL] [DEFAULT *default_value*
| AUTO_INCREMENT] [PRIMARY KEY] [UNIQUE [KEY]]
[COMMENT 'str']
```
```

**index_type:** (see following discussion)

**index_option:** (see following discussion)

**reference_definition:**

```
```code
REFERENCES *tbl_name* (index_columns)
[ON DELETE *reference_action*]
[ON UPDATE *reference_action*]
[MATCH FULL | MATCH PARTIAL | MATCH SIMPLE]
```
```

**reference_action:**

```
```code
RESTRICT | CASCADE | SET NULL | NO ACTION | SET DEFAULT
```
```

**partition_scheme:**

```
```code
PARTITION BY
{
    RANGE (expr)
| LIST (expr)
| [LINEAR] HASH(expr)
| [LINEAR] KEY(*col_list*)
}
[PARTITIONS *n*]
[SUBPARTITION BY
{
    [LINEAR] HASH(expr)
| [LINEAR] KEY(*col_list*)
}
[SUBPARTITIONS *n*]
]
[{*partition_definition* [,*partition_definition*] ...}]
```
```

**partition_definition:**

```
```code
PARTITION *partition_name*
[VALUES (LESS THAN ({*expr*} | MAXVALUE) | IN (*value_list*))]
```
```