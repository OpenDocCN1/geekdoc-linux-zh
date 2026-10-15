
## 警告

这些函数可以向程序返回多个配置值。可以执行的测试总结在下表中。

`pathconf(2)` 和 `fpathconf(2)` 函数以及测试 `_PC_CHOWN_RESTRICTED` 可以检测 `chown(2)` 是否受到限制。这在本章稍后部分介绍。

或者无法通过 `pathconf(2)` 或 `fpathconf(2)` 以及测试 `_PC_CHOWN_RESTRICTED` 来检测 `chown(2)` 是否受到限制。

`pathconf(2)` 和 `fpathconf(2)` 函数以及测试 `_PC_CHOWN_RESTRICTED` 可以检测 `chown(2)` 是否受到限制。这在本章稍后部分介绍。

### Table 6.2

### Listing 6.2. `pathconf(2)` and `fpathconf(2)` Test

| Test | Description |
| :--- | :--- |
| `_PC_LINK_MAX` | The maximum file link count. |
| `_PC_CANON` | The number of bytes in terminal input. Input must represent a terminal. |
| `_PC_MAX_INPUT` | The number of bytes for which space is available in terminal queue. Input must represent a terminal. |
| `_PC_NAME_MAX` | The maximum of bytes in filename (excludes null bytes). Input must represent a directory. |
| `_PC_PATH_MAX` | The number of bytes in pathname (excludes null bytes). Input must represent a directory. |
| `_PC_PIPE_BUF` | The number of bytes that will be written atomically to a pipe. Input must represent a pipe, or directory. |
| `_PC_CHOWN_RESTRICTED` | Return 1 if appropriate privileges are required for the `chown(2)` syscall, 0 otherwise. Input must represent a file or directory. |
| `_PC_VDABLE` | Returns the terminal character disabling value. |

```c
