

保持在逻辑 0。FIFO 在写入时（wrb=0）使能 FPLD 的输出引脚。这让 FPLD 能够将新数据驱动到 RAM 的数据总线上。数据流如图 8.24a 所示。只要 FIFO 未满，在 FIFO 写入操作期间，RAM 写控制线就会被脉冲拉低（第 90 行）。

第 94–96 行处理从 FIFO 读取数据的情况。在第 94 行，外部 RAM 的输出使能在 FIFO 读取操作期间被拉低，以便 RAM 数据总线驱动器被激活。这让 RAM 能够将数据值驱动到 FPLD 中，如图 8.24b 所示。自然地，我们不希望 FPLD 在同一时间尝试向 RAM 驱动数据，否则其中一个 I/O 引脚可能会烧毁，因此通过将写控制输入保持为高来禁用 FPLD 引脚驱动器（参见第 89 行）。第 95 行和第 96 行分别将数据从 RAM 传递到 FIFO 的输出并使能驱动器。这让 FIFO 输出总线能够驱动请求读取 FIFO 的任何电路。

最后，第 99–117 行定义了一个 LED 解码器，它接收 FIFO 在读取操作期间输出的值并将其显示在 LED 数码管上。

FIFO 可以为 XS95 板编译，使用的引脚分配如下。由于我们必须将信号通过连接到外部 RAM 的 15 条地址线、8 条数据线和 3 条控制线的 XC95108 CPLD 的正确引脚，因此引脚分配比我们通常使用的多得多。

```
NET wrb      LOC=P46;   # B0 argument of XSPORT
NET rdb      LOC=P47;   # B1 argument of XSPORT
NET inp0     LOC=P48;   # B2 argument of XSPORT
NET inp1     LOC=P50;   # B3 argument of XSPORT
NET inp2     LOC=P51;   # B4 argument of XSPORT
NET inp3     LOC=P52;   # B5 argument of XSPORT
NET out0     LOC=P5;
NET out1     LOC=P6;
NET out2     LOC=P7;
NET out3     LOC=P11;
NET csb      LOC=P65;
NET web      LOC=P63;
NET oeb      LOC=P62;
NET data0    LOC=P44;
NET data1    LOC=P43;
NET data2    LOC=P41;
NET data3    LOC=P40;
NET data4    LOC=P39;
NET data5    LOC=P37;
NET data6    LOC=P36;
```

## Listing 8.6 A 4-bit wide FIFO built with an external RAM.

```
001- MODULE fifo
002- TITLE 'FIFO with 16 storage locations'
003-
004- DECLARATIONS
005-
006- "I/O pins for the user-interface of the FIFO
007- wrb        PIN; "active-low write control input
008- rdb        PIN; "active-low read control input
009- inp3..inp0 PIN; "4-bit input bus to FIFO
010- out3..out0 PIN; "4-bit output bus from FIFO
011-
012- "I/O pins to the external RAM
013- csb        PIN ISTYPE 'COM'; "active-low chip select
014- web        PIN ISTYPE 'COM'; "active low write control
015- oeb        PIN ISTYPE 'COM'; "active-low read control
016- data7..data0 PIN ISTYPE 'COM'; "RAM I/O bus
017- address14..address0 PIN ISTYPE 'COM'; "15-bit RAM address
018-
019- "output pins to the LED for diagnostic purposes
020- s6..s0     PIN ISTYPE 'COM';
021-
022- "internal nodes
023- reset      NODE;               "active-high FIFO reset
024- empty      NODE ISTYPE 'COM';  "FIFO empty signal
025- full       NODE ISTYPE 'COM';  "FIFO full signal
026- rdptr3..rdptr0 NODE ISTYPE 'REG'; "read ptr. flip-flops
027- wrptr3..wrptr0 NODE ISTYPE 'REG'; "write ptr. flip-flops
028- rdgeqwr    NODE ISTYPE 'COM';  "rdptr==wrptr?
029- prevop1..prevop0 NODE ISTYPE 'REG'; "previous op flags
030-
031- "some synonyms for groups of signals
032- inp = [inp3..inp0];            "4-bit input to FIFO
033- out= [out3..out0];             "4-bit output from FIFO
034- data= [data3..data0];          "4-bit intfc. to external RAM
035- rdptr = [rdptr3..rdptr0];      "FIFO read pointer
036- wrptr = [wrptr3..wrptr0];      "FIFO write pointer
037- address = [address3..address0]; "4-bit address to ext. RAM
038-
039- EQUATIONS
040-
041- "FIFO READ AND WRITE POINTERS
042- "read pointer logic. Increment pointer when reading
```

Listing 8.6    A 4-bit wide FIFO built with an external RAM. (Cont'd.)
```
043- "non-empty FIFO. If FIFO is empty, reload read pointer
044- "with its current contents. Clear pointer on reset.
045- rdptr := !empty & (rdptr+1) # empty & rdptr;
046- rdptr.CLK = rdb; "read operation updates pointer
047- rdptr.ACLR = reset;
048-
049- "write pointer logic. Increment pointer when writing
050- "non-full FIFO. If FIFO is full, reload write pointer
051- "with its current contents. Clear pointer on reset.
052- wrptr := !full & (wrptr+1) # full & wrptr;
053- wrptr.CLK = wrb; "write operation updates pointer
054- wrptr.ACLR = reset;
055-
056- "check read and write pointers to see if they are equal
057- rdeqwr = (rdptr==wrptr);
058-
059- "FIFO CONTROL LOGIC
060- "reset FIFO if both read and write lines are low
061- reset = !rdb & !wrb;
062- "prevop0=0 if most recent operation was a read or reset
063- "prevop0=1 if most recent operation was a write
064- prevop0 := 1;
065- prevop0.CLK = !wrb;
066- prevop0.ACLR = !rdb; "async. clear on read
067- "prevop0=prevop0 and gets updated whenever there is a
068- "read or a write or a reset.
069- prevop1 := prevop0;
070- prevop1.CLK = wrb & rdb;
071- prevop1.ACLR = reset; "async. clear on reset
072- "FIFO is empty if rdptr=wrptr and most recent op was a read
073- "FIFO is full if rdptr=wrptr and most recent op was a write
074- empty = rdeqwr & !prevop1;
075- full = rdeqwr & prevop1;
076-
077- "INTERFACE TO THE EXTERNAL RAM
078- csb = 0; "lower chip select to activate the external RAM
079- "upper bits of RAM address are 0 since we only use
080- "16 locations for the FIFO
081- [address4..address4] = 0;
082- "lower 4 bits come from read or write pointer depending
083- "upon whether it is a read of the FIFO or not.
084- address = !rdb & rdptr # rdb & wrptr;
085- "input data to the FIFO is passed to the external RAM,
```
