
```vhdl
053-       "1111";

054- w0 <= w(0);

055- w1 <= w(1);

056- w2 <= w(2);

057- w3 <= w(3);

058-

059- -- buffer the input clock

060- u4: IBUF PORT MAP(I=>clk, O=>in_clk);

061- u5: BUFG PORT MAP(I=>in_clk, O=>buf_clk);

062-

063- -- this process loads the selected reg on the rising clock edge

064- PROCESS (buf_clk,w0,w1,w2,w3,inp)

065- BEGIN

066- IF(buf_clk'EVENT AND buf_clk='1') THEN

067-   IF w0='0' THEN

068-     rga <= inbus;

069-   END IF;

070-   IF w1='0' THEN

071-     rgb <= inbus;

072-   END IF;

073-   IF w2='0' THEN

074-     rgc <= inbus;

075-   END IF;

076-   IF w3='0' THEN

077-     rgd <= inbus;

078-   END IF;

079- END IF;

080- END PROCESS;

081-

082- outp <= rga WHEN a="00" ELSE    -- select one of the four

083-         rgb WHEN a="01" ELSE    -- registers and output

084-         rgc WHEN a="10" ELSE    -- its value on the output bus

085-         rgd;

086-

087- -- display the output value on the LED display

088- u6: leddcd PORT MAP (d=>outp,s=>s);

089-

090- END mem2_arch;
```

![](img/5124daf79d2807d81e49f49c22f1f8c1_304_0.png)

#### Figure 8.20 同步存储器的仿真波形。

XS95 和 XS40 板的实现方式将相同。以下是可使用同步存储器执行的一些操作示例：

| Action | `XSPORT` Command Sequence |
|---|---|
| Write location 1 (01) with 7 (0111) | `XSPORT 01110100`<br>`XSPORT 01110101` |
| Write location 3 (11) with 10 (1010) | `XSPORT 10101100`<br>`XSPORT 10101101` |
| Read location 0 (00) | `XSPORT 0011` |
| Read location 2 (10) | `XSPORT 1011` |

`MEM2` 设计使用了 XC95108 CPLD 的 51 个宏单元。由于 LED 解码器使用了 7 个宏单元，4×4 存储器必须使用其余的 51 − 7 = 44 个宏单元。这是 CPLD 总资源的大部分。显然，使用本节或上一节所示的技术无法构建非常大的存储器。

### 使用内置存储器

为了让设计人员在设计中使用更大容量的存储器，XC4000 系列 FPGA 配备了内部 RAM。由于 FPGA 中的 LUT 本质上是存储逻辑真值表的 RAM（请回顾图 2.6），因此合理地允许设计人员将这些 RAM 用于通用数据存储。XC4000 FPGA 中的每个 CLB 都有 2 个可作为 RAM 使用的 LUT（图 2.7）。每个 4 输入 LUT 可存储 2⁴=16 位，因此单个 CLB 可存储 32 位数据。数据可以组织为 16×2 RAM、32×1 RAM 或双 16×1 RAM。

（不幸的是，XC9500 系列 CPLD 不提供将宏单元用作逻辑或存储器的选项。因此，本节内容与使用 XS95 板的用户无关。抱歉。）

清单 8.5 显示了一些使用由两个 16x2 内置 RAM 构成的 `RAM16X4` RAM 模块的 VHDL 代码。该模块的 `COMPONENT` 声明在第 20-28 行，是通过查看 `Xilinx\Synth\xilinx\macros\Xc4000e\v6_xnf` 目录下的 `RAM16X4.V6X` 文件确定的。RAM 模块具有 4 位输入和输出总线、4 位地址总线，以及一个高电平有效的写使能输入。

RAM 模块在第 52-58 行被实例化。由于我们只构建一个 4x4 存储器，因此只需要两个地址位。因此，在第 54 行，模块的下两个地址输入连接到地址总线。由于不需要，上两个地址位连接到在第 49 行保持逻辑 0 的 `gnd` 信号。

由于我们针对的是 XS40 板，因此需要从 XC4005XL FPGA 的模式引脚获取部分输入。这在第 43-46 行完成。从模式引脚输入的信号与 2 位输入总线连接起来形成 4 位 `inb` 总线。`inb` 总线在第 55 行连接到 RAM 模块。RAM 模块的剩余输出和写使能端口连接到 `mem3` 设计中的对应信号（第 56 行和第 57 行）。

图 8.21 显示了 `MEM3` 设计的仿真波形。对存储器进行了四次写入，通过施加地址和数据值，然后在 `WE` 输入上放置一个正脉冲。在 0-110 ns 的间隔内，十六进制值 `0xC`、`0x3`、`0x5` 和 `0xA` 分别写入存储器位置 0、1、2 和 3。然后在 120 ns 到 160 ns 之间将这些值读回这些位置。从每个位置读出的值与写入其中的数据相匹配，因此存储器似乎工作正常。

`MEM3` 设计的用户约束文件如下：

```text
NET we              LOC=P44;    # B0 argument of XSPORT

#### NET NE oe          LOC=P45;    # OE is not used with the internal memories

NET a<0>             LOC=P46;    # B2 argument of XSPORT

NET a<1>             LOC=P47;    # B3 argument of XSPORT

NET inpc<0>          LOC=P48;    # B4 argument of XSPORT

NET inpc<1>          LOC=P49;    # B5 argument of XSPORT

#### NET inpc<2>         LOC=P32;    # B6 argument of XSPORT

#### NET inpc<3>         LOC=P34;    # B7 argument of XSPORT

NET s<0>             LOC=P25;    # S0 LED segment

NET s<1>             LOC=P26;    # S1 LED segment

NET s<2>             LOC=P24;    # S2 LED segment

NET s<3>             LOC=P20;    # S3 LED segment

NET s<4>             LOC=P23;    # S4 LED segment
```

#### 清单 8.5 使用内置 FPGA 存储器构建的 4 位宽异步存储器的 VHDL 版本。（续。）

```vhdl
042- u0: md0 PORT MAP (MD0=>MD0in); -- connect the mode inputs to

043- u0: md2 PORT MAP (MD2=>MD2in); -- the bus feeding the RAM module

044- u2: IBuf PORT MAP (I=>MD0in, O=>MD0out);

045- u3: IBuf PORT MAP (I=>MD2in, O=>MD2out);

046- inb <= MD2out & MD0out & inp(1 DOWNTO 0); -- concatenate bits into bus

047-

048- gnd <= '0'; -- connect signal to logic 0;

049-

050- -- connect the RAM16X4 component I/O to the I/O of this module

051- u4: ram16x4 PORT MAP

052-       (

053-         A0=>a(0), A1=>a(1), A2=>gnd, A3=>gnd,       -- connect address bus
```
