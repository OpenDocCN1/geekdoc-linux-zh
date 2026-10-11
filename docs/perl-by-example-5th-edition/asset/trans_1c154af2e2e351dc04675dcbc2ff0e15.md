

## 表 A.1 Perl 函数（续）

| 函数 | 描述                                                                                                                        |
|-------------|--------------------------------------------------------------------------------------------------------------------------------------|
| system      | `system(LIST)`<br>`system LIST`                                                                                                 <br><br>从 Perl 脚本中执行 shell 命令并返回。类似于 `exec` 函数，但它首先会 `forks`（分叉），然后脚本等待命令执行完毕。随后控制返回到脚本。返回值是程序的退出状态，可以通过除以 256 或右移低 8 位来获得。<br>参见 `system`(3)。                                              |

| 函数 | 描述                                                                                                                        |
|-------------|--------------------------------------------------------------------------------------------------------------------------------------|
| syswrite    | `syswrite(FILEHANDLE, SCALAR, LENGTH, OFFSET)`<br>`syswrite(FILEHANDLE, SCALAR, LENGTH)`<br>`syswrite(FILEHANDLE, SCALAR)`                                                    <br><br>返回写入 `FILEHANDLE` 的字节数。如果指定了 `OFFSET`，则从 `OFFSET` 位置开始，将变量 `SCALAR` 中的 `LENGTH` 字节写入 `FILEHANDLE`。使用 `write` 系统调用。<br>参见 `write`(2)。                                                  |

| 函数 | 描述                                                                                                                        |
|-------------|--------------------------------------------------------------------------------------------------------------------------------------|
| tell        | `tell(FILEHANDLE)`<br>`tell FILEHANDLE`                                                                                               <br><br>返回 `FILEHANDLE` 的当前文件位置（以字节为单位，从字节 0 开始计数）。通常将返回的值传递给 `seek` 函数，以便回到文件中的某个位置。<br>参见 `lseek`(2)。                                                    |

| 函数 | 描述                                                                                                                        |
|-------------|--------------------------------------------------------------------------------------------------------------------------------------|
| telldir     | `telldir(DIRHANDLE)`<br>`telldir DIRHANDLE`                                                                                       <br><br>返回目录结构中 `readdir` 函数的当前位置。`DIRHANDLE`。<br>参见 `directory`(3)。                                                    |

| 函数 | 描述 |
| :--- | :--- |
| tie | `tie`(*VARIABLE, CLASSNAME, LIST*) |
|  | 将 `VARIABLE` 绑定到一个包（`CLASSNAME`），该包将使用方法来提供变量的实现。`LIST` 由传递给 new 方法以构造对象的其他参数组成。最常用于关联数组，将它们绑定到数据库。 |
|  | 这些方法具有预定义的名称，需放置在包内。当关联的变量被获取、存储、销毁等时，预定义的方法会被自动调用。 |
|  | 实现关联数组的包提供以下方法： |
|  | `TIEHASH` $classname, *LIST* |
|  | `DESTROY` Self |
|  | `FETCH` Self, *$key* |
|  | `STORE` Self, *$key* |
|  | `DELETE` Self, *$key* |
|  | `EXISTS` Self, *$key* |
|  | `FIRSTKEY` Self |
|  | `NEXTKEY` Self, *$lastkey* |
|  | 为数组提供的方法包括： |
|  | `TIEARRAY` $classname, *LIST* |
|  | `DESTROY` Self |
|  | `FETCH` Self, *$subscript* |
|  | `STORE` Self, *$subscript*, *$value* |
|  | 为标量提供的方法包括： |
|  | `TIESCALAR` $classname, *LIST* |
|  | `DESTROY` Self |
|  | `FETCH` Self |
|  | `STORE` Self, *$value* |
|  | 示例： |
|  | ```perl
|  | $object = tie $hash, Myhashclass
|  | while ($key, $value)=each ($hash){
|  |     print "$key, $value\n" # 调用 FETCH 方法
|  | }
|  | $object = tie $array, Myarrayclass
|  | $array[0]=5 # 调用 STORE 方法
|  | $object = tie $scalar, Myscalarclass
|  | until $scalar # 调用 DESTROY 方法
|  | ``` |
| tied | `tied` *VARIABLE* |
|  | 返回之前使用 `tie` 函数绑定的对象的引用；如果 `VARIABLE` 未绑定到任何包，则返回 undefined（未定义值）。 |

| 函数 | 描述 |
| :------- | :---------- |
| time | <i>time</i> |
| | 返回一个包含 4 个元素的数组，表示自 1970 年 1 月 1 日 UTC 以来的非闰年秒数。通常与 <i>gmtime</i> 和 <i>localtime</i> 函数一起使用。 |
| | 参见 <i>ctime</i>(3)。 |
| times | <i>times</i> |
| | 返回一个包含 4 个元素的数组，给出进程及其子进程的用户和系统 CPU 时间（以秒为单位）。 |
| | 参见 <i>times</i>(3)。 |
| tr | <i>tr</i>(SEARCHPATTERN/REPLACEMENT/[c|d|d]) |
| | <i>y</i>(SEARCHPATTERN/REPLACEMENT/[c|d|d]) |
| | 将 SEARCHPATTERN 中的字符转换为 REPLACEMENT 中对应的字符。类似于 UNIX <i>tr</i> 命令。 |
| truncate | <i>truncate</i>(FILEHANDLE, LENGTH) |
| | <i>truncate</i>(EXPR, LENGTH) |
| | 将 FILEHANDLE 或 EXPR 截断到指定的 LENGTH。 |
| | 参见 <i>truncate</i>(2)。 |
| uc | <i>uc</i> EXPR |
| | 返回 EXPR（如果没有 EXPR 则为 `$_`）的大写形式。等同于 /\uE 转义序列。 |
| ucfirst | <i>ucfirst</i> EXPR |
| | 返回 EXPR（如果没有 EXPR 则为 `$_`）的第一个字符的大写形式。等同于 /\u 转义序列。 |
| umask | <i>umask</i>(EXPR) |
| | <i>umask</i> EXPR |
| | <i>umask</i> |
| | 设置进程的文件创建掩码（<i>umask</i>）并返回旧的 <i>umask</i>。如果省略 EXPR，则返回当前的 <i>umask</i> 值。 |
| | 参见 <i>umask</i>(2)。 |
| undef | <i>undef</i>(EXPR) |
| | <i>undef</i> EXPR |
| | <i>undef</i> |
| | 使 EXPR（一个左值）变为未定义。用于标量、数组、哈希或子例程名称（\&subroutine）以回收与其相关的存储。始终返回未定义值。当从子例程返回时可以使用它本身来确定是否发生了错误。 |

| 函数 | 描述 |
| :------- | :---------- |
| `unlink` | `unlink(LIST)`<br>`unlink LIST`<br>`unlink`<br>删除 LIST 中的文件。返回删除的文件数量。如果没有参数，则删除存储在 `$_` 中的值。参见 `unlink`(2)。 |
| `unpack` | `unpack(TEMPLATE, EXPR)`<br>解包表示结构的字符串并将其扩展为数组值，使用 TEMPLATE 获取值的顺序和类型，返回数组值。是 `pack` 的反向操作。 |
| `unshift` | `unshift(LIST)`<br>`unshift`<br>将 LIST 添加到数组的开头。返回新数组中的元素数量。 |
| `untie` | `untie VARIABLE`<br>解除变量与其所绑定的包之间的绑定（untie）。与 `tie` 相反。 |
| `use` | `use MODULE VERSION LIST`<br>`use MODULE LIST`<br>`use MODULE`<br>`use MODULE()`<br>`use pragma`<br>一条编译器指令，将子例程和变量从 MODULE 导入到当前包中。VERSION 是 Perl 的当前版本号。LIST 由当前包要导入的变量和子例程的具体名称组成。如果不想将任何内容导入到命名空间中，请使用空参数。可以在命令行上使用 -m 和 -M 标志代替 use。Pragma（编译 pragma）是一种特殊的模块，可以在编译时影响一组语句的行为。三种常见的 pragma 是 `integer`、`subs` 和 `strict`。 |
| `utime` | `utime(LIST)`<br>`utime LIST`<br>更改文件列表的访问时间和修改时间。LIST 的前两个元素是数值形式的访问时间和修改时间。 |
| `values` | `values(%ASSOC_ARRAY)`<br>`values ASSOC_ARRAY`<br>返回一个由关联数组 ASSOC_ARRAY 中所有值组成的数组，顺序随机。 |

