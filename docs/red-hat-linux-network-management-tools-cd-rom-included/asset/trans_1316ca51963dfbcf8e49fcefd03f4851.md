
对于该特性，脚本需要一种方式来修改任何被更改的 OID 对象。因为它已经使用 `passpersist.log` 文件作为临时存储，所以它只需要解析此文件并修改脚本中包含的 OID 值。完成此操作后，脚本应删除日志文件中先前解析的条目，以防止在请求另一次设置操作时将其错误地视为新条目。正如你所见，当前版本的 `passpersist` 脚本并未实现永久的 `set-requests`。当使用 `passpersist` 脚本支持的 OID 对代理运行 SNMP `getnext-request` 操作时，将显示以下内容：

```
Enterprises.ucdavis.255.1 = 	"life the universe and everything"
	Enterprises.ucdavis.255.2 =	42
	Enterprises.ucdavis.255.2 =	OID: 42.42.42
	Enterprises.ucdavis.255.3 =	Timeticks: (363136200) 42 days,
	0:42:42.00
	Enterprises.ucdavis.255.4 =	IpAddress: 1.0.0.127
	Enterprises.ucdavis.255.5 =	42
	Enterprises.ucdavis.255.6 =	Gauge: 42
```

列表 7.2 显示了 `pass` 命令的另一个示例。在此程序中，名为 `maintain-message.pl`，SNMP `set-request` 操作被用作触发器来删除系统消息文件的内容。此脚本代表了 `pass` 设施如何帮助执行一些有用的系统管理任务的功能示例。在此示例中，脚本有助于在多台系统上维护 `/var/log/messages` 文件。

## 列表 7.2 Perl 脚本 (maintain-message.pl) 用于维护 messages 文件

```
1  #!/usr/bin/perl -w
2  ###############################################
3  #
4  # Extensible Agent Script Example - Maintenance of the
5  # /var/log/messages file. It
6  # provides a way to delete the contents of the file to zero bytes
7  # and also shows the
8  # the last 50 lines of the file.
9  # Steve Maxwell
10 # December '99
11 #
12  #
13  $MESSAGESFILE = "/var/log/messages";
14  $OID_PATHBASE = "1.3.6.1.4.1.2021.255";
15  $SET_OID    = "1.3.6.1.4.1.2021.255.51";
16  $SET_OID_OBJ   = 51;
17  $DEF_LINES   = 50;
18  $LOG_NAME     = "agent-log";
19  $LOG_PATH     = "/etc/snmp/";
20  $DATE        = "/bin/date '+Date: %m/%d/%y  Time: %H:%M:%S':";
21  $TAIL        = "/usr/bin/tail -n";
22  $LOGGING     = 1;
23  ##
24  ##  Creates logfile.  On success, return 0, else 1.
25  ##
26  sub CreateLogFile {
27
28      $lf = sprintf("%s%s", $LOG_PATH, $LOG_NAME);
29      unless (open (LFP, ">$lf")) {
30          print "Can't open log file: $lf\n";
31          exit 1;
32      }
33      return 0;
34  }
35  ##
36  ##  Logs any string passed to it.
37  ##
38  sub Log {
39      if ($LOGGING) {
40          print LFP " $DATE  $_[0]\n";
41      }
42  }
43  ##
44  ##  Close open log file and exit program with supplied
45  ##  error code.
46  ##
47  sub Leave {
48      close LFP;
49      exit $_[0];
50  }
51  ##
52  ##  We need to purge the log file, but we need to make
53  ##  sure the correct OID string is provided to us.
54  ##
55  sub SnmpSet {
56      ($oid, $type, $value) = @_;
57
58
59  ##  ##  Make sure OID from agent matches are OID set object.
60  ##  ##  if so, then we know to execute the SET operation.
61  ##
62  if($oid eq $SET_OID) {
63          Log "SnmpSet: oid...$oid, type...$type, and value...$value";
64    $comm = sprintf("%s %s %s", "/bin/cp", "/dev/null",
        $MESSAGESFILE);
65    Log "Executing... $comm";
66    $rc = system ($comm);
67    $stat = $rc/256;
68    if ( $stat ) {
69        Log "SnmpSet: Command executes successfully";
70        Leave 0;
71    }
72    }
73    Leave 1;
74    }
75    ##
76    ## Get the next OID and line from the messages
77    ## file.
78    ##
79    sub SnmpGetNext {
80    ($Reqoid, $master_oid) = @_;
81
82    @data = `$TAIL $DEF_LINES $MESSAGESFILE`;
83
84    if ($Reqoid eq $master_oid) {
85        Log "SnmpGetNext: OIDs are equal\n";
86        print "$Reqoid.0\n";
87        print "string\n";
88        print "$data[0]";
89        Log "SnmpGetNext: $Reqoid.0, string, $data[0]";
90        Leave 0;
91    } else {
92    $newstring = "";
93    $oidstring = $Reqoid;
94    (@oids) = split (/\./, $oidstring);
95    $count = @oids-1;
96    for ($i = 1; $i <= $count; $i++) {
97        $newstring = sprintf("%s.%s", $newstring,
        $oids[$i]);
98    }
99    $lastoid = $oids[$#oids];
100    $oid_int = sprintf("%i", $lastoid);
101    $oid_int++;
102    print "$newstring.$oid_int\n";
103    print "string\n";
104    print "$data[$oid_int]";
105    Log "SnmpGetNext: $newstring.$oid_int, string,
        $data[$oid_int]";
106    }
107    Leave 0;
108    }
109    ##
110    ## Get an individual line of the messages file
111    ##
112    sub SnmpGet {
113    $Reqoid = $_[0];
114
115 Log "SnmpGet: $Reqoid";
116 @lines = `$TAIL $DEF_LINES $MESSAGESFILE`;
117
118 (@oids) = split (/\./,$Reqoid);
119
120 $lastoid = $oids[$#oids];
121 if ( $lastoid =~ /$SET_OID_OBJ/ ) {
122 print "$Reqoid\n";
123 print "integer\n";
124 print "0";
125 Leave 0;
126 }
127 if ( $lastoid > 0 && $lastoid < 50 ) {
128 print "$Reqoid\n";
129 print "string\n";
130 print "\n$lines[$lastoid]";
131 Log "SnmpGet: $Reqoid, string, $lines[$lastoid]";
132 Leave 0;
133 } else {
134 Leave 1;
135 }
136 }
137 ##
138 ## Main program starts here
139 ##
140
141 CreateLogFile;
142
143 ($arg1, $arg2, $arg3, $arg4) = @ARGV;
144
145 if ($arg1 eq "-s") {
146 SnmpSet $arg2, $arg3, $arg4;
147 } elsif ($arg1 eq "-n") {
148 SnmpGetNext $arg2, $OID_PATHBASE;
149 } else {
150 SnmpGet $arg2;
151 }
```

此示例由于行数较多看起来可能有些复杂，但实际上该程序非常直接且简单。此外，名为 `messages.pl` 的示例程序使用 Perl 语言编写，并与解释器的 5.005_03 版本一起使用。程序的核心部分在第 141 行到第 151 行之间，主要部分由多个函数分隔。如你所见，程序使用了三个函数，这些函数模仿了代理调用脚本的方式。函数包括从第 55 行开始的 SnmpSet；从第 79 行开始的 SnmpGetNext；以及从第 112 行开始的 SnmpGet。每当代理接收到 SNMP 操作时，都会调用这些函数。与 passpersist 脚本相比，此示例真正新颖之处在于它支持 SNMP set-request 操作。在这种情况下，对特定 OID (1.3.6.1.4.1.2021.255.51) 使用的 set 操作将导致 /var/log/messages 文件的内容被清除。实际命令位于第 64 行。在该行中，使用 $comm 变量调用 system 命令。在 Perl 中，system 命令会将字符串直接发送到操作系统以执行。此变量被赋值为字符串 /bin/cp /dev/null /var/log/messages。函数的其余部分仅检查 system 命令的返回状态并记录脚本活动。如果命令成功，脚本将以成功值终止；否则，它将返回错误状态（第 73 行）。一个名为 leave 的函数用于在退出脚本之前关闭日志文件并返回正确的退出条件。该函数定义在第 47 行和第 50 行。

messages.pl 脚本还提供了一种查看 messages 文件中最多 50 行内容的方法。访问此文件内容的方式是对 MIB 对象 1.3.6.1.4.1.2021.255.1 执行 getnext-request。请记住，getnext 操作会“遍历” MIB 树以检索整个 MIB 或一组 MIB 对象。因此，我们可以获取 255 树下的所有对象。结果，示例输出将如列表 7.3 所示生成。引号中的字符串代表来自 /var/log/messages 文件的实际行。

## 列表 7.3 对 /var/log/messages 文件的 SNMP “walk”

```
enterprises.ucdavis.255.0 = *Sep 1 20:04:30 socrates chat[995]: expect (OK)"
enterprises.ucdavis.255.1 = *Sep 1 20:05:15 socrates ppd[993]: Connect script failed"
enterprises.ucdavis.255.2 = *Sep 1 20:05:15 socrates chat[995]: Fail"
enterprises.ucdavis.255.3 = *Sep 1 20:05:15 socrates chat[995]: Fail"
enterprises.ucdavis.255.4 = *Sep 1 20:05:16 socrates ppd[993]: exit"
enterprises.ucdavis.255.5 = *Sep 1 20:05:16 socrates lwp-upp: ppdpd started for ppdpd on /dev/modem at 115200"
enterprises.ucdavis.255.6 = *Sep 1 20:05:16 socrates ppd[1000]: ppd 2.3.7 started by root, uid 0"
enterprises.ucdavis.255.7 = *Sep 1 20:05:17 socrates ppd[1000]: up on (BUSY)
enterprises.ucdavis.255.8 = *Sep 1 20:05:17 socrates chat[1002]: abort on (ERROR)"
enterprises.ucdavis.255.9 = *Sep 1 20:05:17 socrates chat[1002]: abort on (NO CARRIER)"
enterprises.ucdavis.255.10 = *Sep 1 20:05:17 socrates chat[1002]: abort on (NO DIALTONE)"
enterprises.ucdavis.255.11 = *Sep 1 20:05:17 socrates chat[1002]: (Invalid Login)"
```

(续)

