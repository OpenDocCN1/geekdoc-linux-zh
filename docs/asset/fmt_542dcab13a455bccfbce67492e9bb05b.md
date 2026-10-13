
# 3. 运行 tip

注意。切勿从 `emtool` 运行 `tip`。使用 `shelltool`、`xterm` 或其他没有滚动条的窗口。滚动条会干扰 `tip` 对 `Return` 键的处理。

此警告也有例外，但如果你从不在带滚动条的窗口中运行 `tip`，你就不需要记住所有它失效的情况了。

- a. 现在，使用你在 `/etc/remote` 中编辑过的 `hardwire` 条目，输入 `tip hardwire`（或 `tip hardwire2`）并按 `Return`。
你应该会看到 `connected`。

- b. 输入 `ATE1` 并按 `Return`。
（这适用于所有兼容 Hayes 的调制解器，甚至是更便宜的型号。）
你应该看到 `OK`。恭喜！你正在与调制解器通信！

- c. 现在，发送适当的 AT 命令来为调制解器编程。
（参见第 694 页的“基础调制解器编程”）。

## Tip 和 /etc/remote 693

- d. 不要忘记将新设置写入调制解器的非易失性 RAM（NonVolatile RAM）。

如果你没有看到 `OK`，说明你没有与调制解器通信。检查调制解器是否连接，验证调制解器的波特率以及 `/etc/remote` 中的 `hardwire` 条目，并检查调制解器电缆。

4. 按 `Return ~` 退出 `tip`。
这意味着依次输入三个单独的键：`Return`、`波浪`、`句号`。此步骤也会退出登录，因此如果你是通过 `login` 运行 `tip`，请使用 `Return --`（`Return`、`波浪`、`波浪`、`句号`），否则你只会退出登录。

下方 `/etc/remote` 示例中的 `cuaa` 条目允许你输入 `tip cuaa` 并直接与端口 A 上以 19200 bps 运行的调制解器通信，使用 7 位、偶校验。

`cuab` 条目（在下方示例）允许你输入 `tip cuab` 并直接与端口 A 上以 9600 bps 运行的调制解器通信，使用 8 位、无校验。

`tip some_phone_number` 查找 `tip0` 条目并使用该定义通过 19200 bps、7 位、偶校验连接拨打 `some_phone_number`。（在下方的 `/etc/remote` 示例中，它使用 `tip0`，`tip0` 指向 `UNIX-19200`，设置了一个拨号 19200 bps、7 位、偶校验、兼容 Hayes 的调制解器。`UNIX-19200` 指向 `diala`，`diala` 引用了 `/dev/cua/a`。复杂对吧？）

`tip mysystem`（下方）查找 `mysystem` 条目并通过 `/dev/cua/a` 上的 19200 bps、7 位、无校验连接拨打号码 1415551234。

# /etc/remote 示例

以下示例 `/etc/remote` 文件配置用于：

- 端口 a，19200 bps，兼容 Hayes 的调制解器，7 位，偶校验。（因为没有 `p8` 条目，所以是 7E1）。
- 端口 b，9600 bps，兼容 Hayes 的调制解器，8 位，无校验。（因为有 `p8` 条目，所以是 8N1）。

查看 `remote(4)` 获取所有可能的选项。

```
cuaa=/dev/cua/a;br#19200:

cuab=/dev/cua/b;br#9600

mysystem=1415551234:tc=UNIX-19200:

    :dev=/dev/cua/b:br#9600:el="C"S"Q"O";ie=5e:od=

tip0=UNIX-19200:

tip960=UNIX-19200:

UNIX-900:

    el="C"S"Q"O";du:at=hayes:ie=%5%;:od=br#9600:tc=dial

UNIX-19200:

    el="C"S"Q"O";du:at=hayes:ie=%5%;:od=br#19200:tc=diala

diala=*

:dv=/dev/cua/a:

dialb:

:dv=/dev/cua/b:
```
