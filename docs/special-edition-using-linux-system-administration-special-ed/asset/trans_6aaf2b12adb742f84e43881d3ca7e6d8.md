
```
97: Syslog facility name for ServerTracing messages [daemon]?
98: Set UID to 0 to manipulate LOCAL [""]?

99: Your facsimile phone number (+972.4.8331039) does not agree with your
100: country code (972) or area code (4).
101: should be a fully qualified international dialing number of the form:

102: +972 4 <local phone number>

103: Spaces, hyphens, and periods can be included for legibility. For example,

104: +972.4.555.1212

105: is a possible phone number (using your country and area codes).

106: The non-default server configuration parameters are:

107: CountryCode:          972
108: AreaCode:             4
109: FAXNumber:            +972.4.8331039
110: LongDistancePrefix:   0
111: InternationalPrefix:  00
112: DialStringRules:      etc/dialrules
113: SessionTracing:        11
114: RingsBeforeAnswer:     1
115: SpeakerVolume:         off
116: GettyArgs:             "-h %s -b %s"
117: LocalIdentifier:       "MyFaxServer"
118: TagLineFont:           etc/lutRS18.pcf
119: TagLineFormat:         "From %s|%c|Page %sP of %sT"
120: MaxRecvPages:          25

121: Are these ok [yes]?

122: Now we are going to probe the tty port to figure out the type
123: of modem that is attached. This takes a few seconds, so be patient.
124: Note that if you do not have the modem cabled to the port, or the
125: modem is turned off, this may hang (just go and cable up the modem
126: to turn it on, or whatever).

127: Probing for best speed to talk to modem: 38400 OK.

128: This modem looks like to have support for both Class 1 and 2;
129: how should it be configured [2]? 1

130: Hmm, this looks like a Class 1 modem.
131: Product code (ATI0) is "28800".
132: Other information (ATI3) is "V1.302-V34_DP".
133: DTE-DCE flow control scheme [default]?
134: grep: defaults: Is a directory
135: Modem manufacturer is "ROCKWELL".
136: Modem model is "RC288DPi".

137: Using prototype configuration file rc288dpi-1...
138: The modem configuration parameters are:

139: ModemDialCmd:        ATDT%s
140: ModemFlowControl:    rtscts
141: ModemHardFlowCmd:    AT&K3
142: ModemMfrQueryCmd:     !Rockwell
143: ModemModelQueryCmd:   !RC288?Di
144: ModemNoFlowCmd:       AT&K0
145: ModemRate:            38400
146: ModemRevQueryCmd:     AT13
147: ModemSetupDCDCmd:     AT&C1
148: ModemSetupDTRCmd:     AT&D2
149: ModemSoftFlowCmd:     AT&K4

150: Are these ok [yes]?

151: Creating new configuration file /var/spool/fax/etc/config.ttyS1...
152: Creating fifo /var/spool/fax/FIFO.ttyS1 for faxgetty... done.
153: Done setting up the modem configuration.

154: Checking /var/spool/fax/etc/config for consistency...
155: ...some parameters are different.

156: The non-default scheduler parameters are:

157: CountryCode:          972
158: AreaCode:             4
159: LongDistancePrefix:   0
160: InternationalPrefix:  00
161: DialStringRules:      etc/dialrules
162: MaxSendPages:         25

163: Are these ok [yes]?

164: Creating new configuration file /var/spool/fax/etc/config...
165: ...saving current file as /var/spool/fax/etc/config.sav.

166: Don't forget to run faxmodem(1M) (if you have a send-only environment)
167: or configure init to run faxgetty on ttyS2.
168: Do you want to run faxaddmodem to configure another modem [yes]? no

169: You do not appear to be using faxgetty to notify the HylaFAX scheduler
170: about new modems and/or their status. This means that you must use the
171: faxmodem program to inform the new fax process about the modems you
172: want to have scheduled by HylaFAX. Beware that if you have modems that
173: require non-default capabilities specified to faxmodem then you should
174: read faxmodem(1M) manual page and do this work yourself (since this
175: script is not intelligent enough to automatically figure out the modem
176: capabilities and supply the appropriate arguments).

177: Should I run faxmodem for each configured modem [yes]?
178: /usr/sbin/faxmodem ttyS1

179: Done verifying system setup.
180: #
```

本次会话可作如下分析：

- 在第6-23行，faxsetup程序发出找不到vgetty和egetty程序的警告。这些警告可以安全忽略。
- 在第24行，faxsetup指示需要从`/var/spool/fax/bin/ps2fax`创建一个指向`/var/spool/fax/bin/ps2fax.gs`的软链接。Linux系统使用ghostscript作为成像引擎，而不是其他默认程序。RPM安装会自动处理此事，可以安全忽略，除非你是从源代码编译并安装HylaFAX的。
- 在第25-27行，创建fax用户。HylaFAX以该用户身份运行其守护进程。然而，当你之后用ps检查进程时，会发现HylaFAX守护进程以用户uucp身份运行。这没问题，HylaFAX创建fax用户时使用了与uucp相同的UID。
- 在第28和29行，faxsetup告知你它写入调制解调器支持函数和配置参数的文件名。如果你之后需要调整这些文件中的任何值，这是有用的信息。
- 在第31-34行，你向faxsetup提供传真调制解调器的国家代码、区号和本地电话号码。
- 在第45行，你有机会更改传出传真作业的最大页数。
- 在第54行，faxsetup告知你新配置文件保存的位置。
- 在第55-58行，通过运行脚本`/etc/rc.d/init.d/hylafax`启动HylaFAX守护进程hfaxd和faxq。同时也会告知你这些守护进程不支持较旧的传真协议或SNPP。如果你需要支持较旧的传真客户端或寻呼机，必须从源代码重新编译并启用这些选项。
- 在第61和62行，系统提示你运行faxaddmodem程序。该程序查询连接传真调制解调器的串行端口，然后继续配置它以供HylaFAX使用。
- 在第71-98行，配置连接到第62行指定的串行端口上的调制解调器。
- 在第99-120行，显示当前配置。在第121行，系统提示你接受配置或进行修改。
- 在第122-149行，faxsetup运行probemodem程序，并尝试了解其所有能力。此部分的输出是特定于调制解调器的，可能与你的faxsetup输出不匹配。
- 在第150行，系统提示你接受调制解调器配置参数。接受后，配置被写入，并告知其位置。
- 在第151行，创建一个供HylaFAX使用的FIFO缓冲区。
- 在第164和165行，配置文件被保存，任何先前运行产生的旧配置文件都会被备份。
- 在第166和167行，提醒你：如果这是仅发送的调制解调器，则运行`faxmodem`；若要同时发送和接收，则运行`faxgetty`。
- 在第168行，系统提示你配置另一个传真调制解调器。
- 在第177行，此示例中已告知`faxsetup`运行`faxmodem`程序，并在第178行通知用户它已完成此操作。

## 配置 faxgetty

建议在调制解调器端口上运行faxgetty，即使该端口未配置为提供入站服务也是如此。faxgetty在调制解调器使用时通知HylaFAX调度进程，并识别调制解调器的能力，将该信息传递给调度器，调度器利用该信息做出更好的调度决策。此外，faxgetty在重置难以处理的调制解调器方面也表现出色。

要运行faxgetty，你必须编辑/etc/inittab文件，并向该文件添加一行类似于以下内容的行：

```
t2:2345:respawn:/usr/sbin/faxgetty ttyS1
```

> **提示**
>
> 上面的示例假设你的调制解调器连接到`/dev/ttyS1`。如果实际连接的是`/dev/ttyS2`，别忘了将行首的`t2`改为`t3`。串行端口1或`t1`对应`ttyS0`；串行端口2或`t2`对应`ttyS1`，以此类推。不要使用较旧的串行设备，如`/dev/cua0`或`/dev/cua1`。

接下来，按如下方式通知init程序重新扫描/etc/inittab文件：

```
# telinit q
```

现在你可以测试传真服务器了。

## 测试 HYLAFAX

检查HylaFAX守护进程是否正在运行。请记住，出于安全原因，这些守护进程不以root用户身份运行。它们以fax用户身份运行，该用户与uucp用户相同。使用如下ps命令查找传真守护进程：

```
# ps -aef|grep uucp
uucp      331     1  0 14:42 ?        00:00:00 /usr/sbin/faxq
uucp      333     1  0 14:42 ?        00:00:00 /usr/sbin/hfaxd -i hylafax
uucp      396     1  0 14:44 ?        00:00:00 /usr/sbin/faxgetty ttyS1
root      424   378  0 14:48 tty1     00:00:00 /usr/bin/uucp
```

你应该会看到三个守护进程在运行：faxq、hfaxd和faxgetty，如上面的输出所示。
