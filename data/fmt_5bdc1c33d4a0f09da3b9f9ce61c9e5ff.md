
第 55 到 60 行的第二个进程只是在时钟上升沿将 `next_state` 数组中保存的状态值复制到 `curr_state` 数组中。因此，该进程将状态机从当前状态移动到下一个状态。实际的状态锁存器也是在此进程中隐含的。此外，下一个状态受第一个进程中的复位输入影响，但只有在第二个进程更新当前状态时才会生效。这使得复位是同步的。

因此我们必须显式描述时钟输入到其中一个时钟缓冲器的连接。这在第 26 行和第 27 行完成。在第 26 行，主时钟输入连接到一个输入缓冲器 `IBUF` 模块。然后在第 27 行，`IBUF` 模块的输出连接到通用时钟缓冲器 `BUFG` 的输入。`BUFG` 的输出 `buf_c` 成为驱动状态更新进程的时钟。`IBUF` 和 `BUFG` 接口由第 18–21 行的 `COMPONENT` 语句描述。当你针对 `XC4000` FPGA 时，必须使用此时钟输入缓冲电路。对于 `XS95` 板和 `XC9500` CPLD，你可以移除这些缓冲器并直接使用时钟输入。

上/下计数器的模拟波形如图 10.10 所示。`RESET` 输入在 0–10 ns 被激活并将 `{Q1,Q0}` 状态向量复位为 0。当 `RESET` 被释放时，计数器开始向下计数，因为 `UP=0`。计数器在 10–50 ns 的期间按序列 0、2、1、0 进展，并在 2 处回滚。然后我们在 50 ns 时抬高方向控制使 `UP=1`。这使得计数器在 50–100 ns 期间递增。最后，我们在 100 ns 时再次抬高 `RESET`。由于它是同步复位，计数器仅在下一个上升时钟沿 106 ns 时从状态 1 移动到 0。状态机似乎按我们期望的方式工作。

`CNT3` 设计的约束文件应为 `XS40` 板分配输入和输出，如下所示：

```
NET c      LOC=P44;  # B0 argument of XSPORT
NET reset  LOC=P45;  # B1 argument of XSPORT
NET up     LOC=P46;  # B2 argument of XSPORT
NET q0     LOC=P25;  # S0 LED segment
NET q1     LOC=P26;  # S1 LED segment
NET outp0  LOC=P24;  # S2 LED segment
NET outp1  LOC=P20;  # S3 LED segment
```

或使用以下约束用于 `XS95` 板：

```
NET c      LOC=P46;  # B0 argument of XSPORT
NET reset  LOC=P47;  # B1 argument of XSPORT
NET up     LOC=P48;  # B2 argument of XSPORT
NET q0     LOC=P21;  # S0 LED segment
NET q1     LOC=P23;  # S1 LED segment
NET outp0  LOC=P19;  # S2 LED segment
NET outp1  LOC=P17;  # S3 LED segment
```

时钟输入必须分配给 `B0` 或 `B1`。这些输入通过 `XS40` 或 `XS95` 板上的施密特触发器缓冲器，该缓冲器可消除 PC 并行端口信号缓慢转换引起的任何虚假毛刺。使用 `B2–B7` 中的任何一位都可能导致计数器不规则地递减。这对于我们做的任何时序设计都是如此。

### Listing 7.2 3-state up/down 计数器的 VHDL 代码。

```
001- -- 3-state up/down counter
002-
003- LIBRARY IEEE;
004- USE IEEE.std_logic_1164.ALL;
005-
006- ENTITY cnt3 IS
007- PORT
008- (
009- c: IN STD_LOGIC; -- clock input
010- reset: IN STD_LOGIC; -- active-high reset
011- up: IN STD_LOGIC; -- up/down control input
012- outp0, outp1: OUT STD_LOGIC;-- outputs
013- q0,q1: OUT STD_LOGIC -- state outputs
014- );
015- END cnt3;
016-
017- ARCHITECTURE cnt3_arch OF cnt3 IS
018- COMPONENT IBUF PORT(I: IN STD_LOGIC;
019- O: OUT STD_LOGIC); END COMPONENT;
020- COMPONENT BUFG PORT(I: IN STD_LOGIC;
021- O: OUT STD_LOGIC); END COMPONENT;
022- SIGNAL in_c, buf_c: STD_LOGIC;
023- SIGNAL curr_state, next_state: STD_LOGIC_VECTOR(1 DOWNTO 0);
024- BEGIN
025-
026- u0: IBUF PORT MAP(I=>c, O=>in_c);-- connect clock to
027- u1: BUFG PORT MAP(I=>in_c, O=>buf_c);-- clock buffer
028-
029- outp0 <= curr_state(0); -- connect outputs to current state
030- outp1 <= curr_state(1)
031- q0 <= curr_state(0); -- connect state outputs to current state
032- q1 <= curr_state(1);
033-
034- PROCESS(reset,up,curr_state)-- compute next state from current
035- BEGIN
036- IF reset='1' THEN
037- next_state <= "00";
038- ELSIF curr_state="00" THEN
039- IF up='1' THEN next_state <= "01";
040- ELSE next_state <= "10";
041- END IF;
042- ELSIF curr_state="01" THEN
043- IF up='1' THEN next_state <= "10";
044- ELSE next_state <= "00";
045- END IF;
046- ELSIF curr_state="10" THEN
047- IF up='1' THEN next_state <= "00";
048- ELSE next_state <= "01";
049- END IF;
050- ELSE
051- next_state <= "00";
052- END IF;
053- END PROCESS;
054-
055- PROCESS(buf_c,next_state)-- update the current state vector
056- BEGIN
057- IF (buf_c'event AND buf_c='1') THEN
058- curr_state <= next_state;
059- END IF;
060- END PROCESS;
061-
062- END cnt3_arch;
```

![](img/5124daf79d2807d81e49f49c22f1f8c1_230_0.png)

### Figure 7.10 3-state up/down 计数器的仿真波形。

将电路下载到 `XS40` 或 `XS95` 板后，您可以使用以下命令序列在状态机之间移动其各种状态。每一组命令激活特定的输入，然后向状态机发送一个上升时钟边沿。您可以通过观察 `S0` 和 `S1` LED 段读取当前状态。

| Action | XSPORT Command Sequence |
|---|---|
| Reset the counter | `XSPORT 010`<br>`XSPORT 011`<br>`XSPORT 000` |
| Increment by one | `XSPORT 100`<br>`XSPORT 101`<br>`XSPORT 000` |
| Decrement by one | `XSPORT 000`<br>`XSPORT 001`<br>`XSPORT 000` |

## A Drink Dispenser Controller

本示例将向您展示如何设计一个状态机来解决一个实际问题：分发软饮料。

您受聘设计一台软饮料机的逻辑，该机器分发两种品牌的汽水：`Swill` 和 `Krunk`。分配器应接受镍币和硬币，并允许买者在投入 25¢ 后选择其中一种软饮料。这就是要求的全部内容。
