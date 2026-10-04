

## A. 6.4 FPU 指令

FPU 指令有很多带有“-R”或“-P”后缀的派生指令。带有 R 后的指令与常规指令相反，其操作数的排列顺序与常规指令相反。带有 P 后的指令在运行计算后，会从内存里抛出一个数据；带有 PP 后的指令则从内存抛出两个数据。P/PP 后的指令可在计算释放后存储中的计算因子。

- FABS：计算 ST(0) 绝对值的指令。ST(0)=abs(ST(0))。
- FADD op：单因子加法运算指令。ST(0)=ST(0)+op。
- FADD ST (0), ST (i) ：加法运算指令。ST(0)=ST(0)+ST(i)。
- FADDP ST (1) ：相当于 ST(1)=ST(0)+ST(1)；求和之后，再从内存里抛出一个因子。即，使用计算求得的“和”替换计算因子。
- FCHS：减法运算指令。ST(0)=-1ST(0)。
- FCOM：比较 ST(0) 和 ST(1)。
- FCOM op：比较 ST(0) 和 op。
- FCOMP：比较 ST(0) 和 ST(1)；然后执行 1 次出栈操作。
- FCOMPP：比较 ST(0) 和 ST(1)；然后执行 2 次出栈操作。
- FDIV op：ST(0)=op/ST(0)。
- FDIV ST (i), ST (j) ：ST(i)=ST(j)/ST(i)。
- FDIVRP op：ST(0)=op/ST(0)，然后执行 1 次出栈操作。
- FDIVRP ST (i), ST (j) ：ST(i)=ST(j)/ST(i)，然后执行 2 次出栈操作。
- FDIV op：ST(0)=ST(0)/op。
- FDIV ST (i), ST (j) ：ST(i)=ST(j)/ST(j)。
- FDIVP op：ST(1)=ST(0)/ST(1)，然后执行 1 次出栈操作。即，被除数替换为商。
- FILD op: 将整数转化为长精度数据，并存入 ST (0) 的指令。
- FIST op: 将 st (0) 以整数保存到 op。
- FISTP op: 将 st (0) 以整数保存到 op，再从栈里抛出 ST (0)。
- FLD1: 把 1 推入栈。
- FLDCW op: 从 16 位的操作里提取 FPU 控制字（参见附录 A.3）。
- FLD op: 把 op 推入栈。
- FMUL op: ST(0)=ST(0)*op。
- FMUL ST (i), ST (j) : ST(i)=ST(i)*ST(j)。
- FMULP op: ST(0)=ST(0)*op; 然后执行 1 次出栈操作。
- FMULP ST (i), ST (j) : ST(i)=ST(i)*ST(j); 然后执行 1 次出栈操作。
- FSINCOS: 一次计算 Sin 和 Cosine 结果的指令。

调用指令时，ST (0) 存储角度参数 tmp。ST(0)=sin(tmp); PUSH ST(0) (即 ST1 存储 Sin 值); 之后再次计算 ST(0)=cos(tmp)。

- FSQRT: ST(0)=√ST(0)。
- FSTCW op: 检查尚未处理的、未被屏蔽的浮点异常，再将 FPU 的控制字（参见附录 A.3）保存到 op。
- FNSTCW op: 将 FPU 的控制字（参见附录 A.3）直接保存到 op。
- FSTSW op: 检查尚未处理的、未被屏蔽的浮点异常，再将状态字（参见附录 A.3）保存到 op。
- FNSTSW op: 将状态字（参见附录 A.3）直接保存到 op。
- FST op: 保存实数 ST(0) 到 op。
- FSTP op: 将 ST(0) 复制 op，然后执行 1 次出栈操作 (ST(0))。
- FSUBR op: ST(0)=op-ST(0)。
- FSUBR ST (0), ST (i) : ST(0)=ST(i)-ST(0)。
- FSUBRP: ST(1)=ST(0)-ST(1),然后执行 1 次出栈操作。即被减数替换为差。
- FSUB op: ST(0)=ST(0)-op。
- FSUB ST (0), ST (i) : ST(0)=ST(0)-ST(i)。
- FSUSBP ST (1) : ST(1)=ST(1)-ST(0)。
- FUCOM ST (i) : 比较 ST (0) 和 ST (i)。
- FUCOM: 比较 ST (0) 和 ST (1)。
- FUCOMP: 比较 ST (0) 和 ST (1),然后执行 1 次出栈操作。
- FUCOMPP: 比较 ST (0) 和 ST (1),然后从栈里抽出 2 个数据。

上述两个指令与 FCOM 的功能相似，但是它们在处理 QNaN 型数据时不会报错，仅在处理 NaN 时进行异常汇报。

- FXCH ST (i) : 交换 ST (0) 和 ST (i) 的数据。
- FXCH: 交换 ST (0) 和 ST (1) 的数据。

## A. 6.5 可显示的汇缩指令(32位)

在构建 Shellcode 时（参见第82章），用到下面这个表：

| ASCII字符 | 16 进制码 | x86指令 |
| :--- | :--- | :--- |
| 0 | 30 | XOR |
| 1 | 31 | XOR |
| 2 | 32 | XOR |
| 3 | 33 | XOR |
| 4 | 34 | XOR |
| 5 | 35 | XOR |
| 7 | 37 | AAA |
| 8 | 38 | CMP |
| 9 | 39 | CMP |
| : | 3A | CMP |
| ; | 3B | CMP |
| < | 3C | CMP |
| = | 3D | CMP |
| ? | 3F | AAS |
| @ | 40 | INC |
| A | 41 | INC |
| B | 42 | INC |
| C | 43 | INC |
| D | 44 | INC |
| E | 45 | INC |
| F | 46 | INC |
| G | 47 | INC |
| H | 48 | DEC |
| I | 49 | DEC |
| J | 4A | DEC |
| K | 4B | DEC |
| L | 4C | DEC |
| M | 4D | DEC |
| N | 4E | DEC |
| O | 4F | DEC |
| P | 50 | PUSH |
| Q | 51 | PUSH |
| R | 52 | PUSH |
| S | 53 | PUSH |
| T | 54 | PUSH |
| U | 55 | PUSH |
| V | 56 | PUSH |
| W | 57 | PUSH |
| X | 58 | POP |
| Y | 59 | POP |
| Z | 5A | POP |
| [ | 5B | POP |
| \ | 5C | POP |
| ] | 5D | POP |
| ^ | 5E | POP |
| - | 5F | POP |
| ' | 60 | PUSHA |
| a | 61 | POP |
| f | 66 | POP |
| g | 67 | POP |
| h | 68 | PUSH |
| i | 69 | IMUL |
| j | 6a | PUSH |
| k | 6b | IMUL |
| p | 70 | JO |
| q | 71 | JNO |
| r | 72 | JB |
| s | 73 | JAE |
| t | 74 | JE |
| u | 75 | JNE |
| v | 76 | JBE |
| w | 77 | JA |
| x | 78 | JS |
| y | 79 | JNS |
| z | 7A | JP |

