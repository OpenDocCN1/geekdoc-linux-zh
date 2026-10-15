

# 1.11.2 关于终端的一些说明

我们的程序需要以反白（reverse video）模式显示提示符。问题在于，我们如何在终端上以反白模式显示文本。终端是一个复杂的主题，我们将在后面用将近一整章（第4章）来专门讨论。现在，我们仅对它们做个简要介绍。

终端通常扮演两个角色：它既是输入设备，也是输出设备。作为输出设备，可以向其发送特殊代码，终端不会将这些代码视为要显示的实际文本，而是将其视为控制序列——即一系列字节，告诉它如何定位光标、如何显示文本、如何滚动、是否换行、使用什么颜色等等。在终端最初发展时期，有许多不同的类型和众多厂商。每种类型都有一套不同的控制序列。1976年，欧洲计算机制造商协会（ECMA）对可发送到终端的序列集合进行了标准化。该标准历经多次更新，最终被国际标准化组织（ISO）和国际电工委员会（IEC）采纳，命名为ISO/IEC 6429。该标准后来也被美国国家标准学会（ANSI）采纳，称为ANSI X3.64。如今这些序列集合通常被称为ANSI转义序列，尽管ANSI已于1997年撤销了该标准。

ANSI转义序列是一串ASCII字符，其中前两个通常是ASCII转义字符（十进制代码为27）和左方括号字符“ [”。转义字符可用八进制记法写为`'\033'`。字符串`"\033["`被称为控制序列引入器（Control Sequence Introducer），简称CSI。CSI后面的一个或多个字符指定一个字母数字代码，用于控制键盘或显示功能。例如，序列`"\033[7m"`就是CSI后跟控制代码`"7m"`。代码`"7m"`是反转视频显示（反白）的代码。转义序列`"\033[m"`则关闭之前所有的字符代码。

如果我们想以反白模式显示一段文本（比如提示符），就需要将转义序列和文本发送到终端设备。任何能够写入终端的输出函数都可以胜任。我们使用`printf()`函数，因为它是最简单的。要以反白模式写入提示符“ more? ”，我们需要先发送第一个转义序列，然后发送提示符，最后发送恢复终端的序列：

```
printf("\033[7m more? \033[m");
```

尽管前面的讨论围绕着终端展开，但你在shell中工作时，使用的很可能并不是真正的终端。更有可能的是，你使用的是终端仿真软件包，例如Linux上的GNOME Terminal或Konsole；如果是远程连接，则可能是PuTTY之类的软件。几乎所有运行在Unix系统上的终端仿真器都能解释ANSI转义序列的某个子集。它们用软件来模拟硬件终端的行为。最早支持ANSI转义序列的终端之一是VT100。直到今天，大多数终端仿真器仍支持VT100。有些还支持更高级的终端，如VT102或VT220。原则上，如果终端仿真器支持完整的ANSI转义序列集合，那么无论仿真的是哪种终端，使用这些序列的程序都应该能够正常工作。

前面用于反白显示的代码只是众多可以控制终端的转义序列之一。稍后我们将再探索一些其他的转义序列。

## 清单1.5：more版本1的辅助函数。

```
void do_more_of( FILE *fp )
```
```
{    char      line[LINE_LEN];        // buffer to store line of input    int       num_of_lines = SCREEN_ROWS; // # of lines left on screen    int       getmore     = 1;    // boolean to signal when to stop    int       reply;                // input from user

    while ( getmore && fgets( line , LINE_LEN, fp ) ){
        // fgets() returns pointer to string read or NULL        if ( num_of_lines == 0 ) {
            // reached screen capacity so display prompt            reply = get_user_input();
            switch ( reply ) {
                case SPACEBAR:
                    // allow full screen
                    num_of_lines = SCREEN_ROWS;
                    break;
                case RETURN:
                    // allow one more line
                    num_of_lines++;
                    break;
                case QUIT:
                    getmore = 0;
                    break;
                default:  // in case of invalid input
                    break;
            }
        }
        if ( fputs( line , stdout ) == EOF )
            exit(1);
        num_of_lines--;
    }
}

int get_user_input()
/*
 *  display message, wait for response, return key entered as int
 *  Returns SPACEBAR, RETURN, QUIT, or INVALID
 */
{
    int     c;

    printf("\033[7m more? \033[m"); /* reverse on a VT100     */
    while( (c = getchar()) != EOF )   /* wait for response      */
        switch ( c ) {
            case 'q':               /* 'q' pressed */
                return QUIT;
            case ' ':               /* ' ' pressed */
                return SPACEBAR;
```

