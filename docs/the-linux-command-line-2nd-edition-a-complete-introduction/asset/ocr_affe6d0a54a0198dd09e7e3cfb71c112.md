| Operator | Description |
|---|---|
| `parameter = value` | Simple assignment. Assigns *value* to *parameter*. |
| `parameter += value` | Addition. Equivalent to `parameter = parameter + value`. |
| `parameter -= value` | Subtraction. Equivalent to `parameter = parameter − value`. |
| `parameter *= value` | Multiplication. Equivalent to `parameter = parameter * value`. |
| `parameter /= value` | Integer division. Equivalent to `parameter = parameter / value`. |
| `parameter %= value` | Modulo. Equivalent to `parameter = parameter % value`. |
| `parameter++` | Variable post-increment. Equivalent to `parameter = parameter + 1` (however, see discussion below). |
| `parameter--` | Variable post-decrement. Equivalent to `parameter = parameter − 1`. |
| `++parameter` | Variable pre-increment. Equivalent to `parameter = parameter + 1`. |
| `--parameter` | Variable pre-decrement. Equivalent to `parameter = parameter − 1`. |

These assignment operators provide a convenient shorthand for many common arithmetic tasks. Of special interest are the increment (++) and decrement (−−) operators, which increase or decrease the value of their parameters by one. This style of notation is taken from the C programming language and has been incorporated by several other programming languages, including bash.

The operators may appear either at the front of a parameter or at the end. While they both either increment or decrement the parameter by one, the two placements have a subtle difference. If placed at the front of the parameter, the parameter is incremented (or decremented) before the parameter is returned. If placed after, the operation is performed after the parameter is returned. This is rather strange, but it is the intended behavior. Here is a demonstration:

```
```bash
[me@linuxbox ~]$ foo=1
[me@linuxbox ~]$ echo $((foo++))
1
[me@linuxbox ~]$ echo $foo
2
```
```