cvvis=\E[34m, dch=\E[31m, dhl=\E[1m, dl=\E[31m,
dl1=\E[1M, ed=\E[1B, el=\E[1K, enacs=\E[1K, en=\E(8B)0,
flash=\E[1m, home=\E(8B, ht=\E[1m, ich=\E[1d0,
lil=\E[1d0, il1=\E[1L, ind=j=\E[2=0, kbs=\177,
kbct=\E[2m, kcub1=EOB, kcud1=EOB, kcuul1=EOA,
ckud1=\E[2m, kend=6, kf1=E1,
kf11=\E[23m, kf12=\E[24m, kf20=\E[2m, kf30=\E[3m, kf40=EOS,
kf45=\E[5m, kf16=\E[6m, kf17=\E[7m, kf18=\E[8m, kf19=\E[9m, kf20=\E,
home1=\E[1m, kihl2=\E[2m, kpn6=\E[6m, kpp=\E[5-
elge=\E[5m, nps3=\E[4m, rtp=\E[7m, rdm, rmace=0,
rrm=\E[10491, rmr=\E[4m, rmkx=\E[11m], rmso=\E[23m,
rrm2=\E[24m, rs2=\E[11m], rmso=\E[23m],

seta=\E[4m, seta1=\E[3m,
seta=\E[0m%6tr=\E[1m; seta1=\E[2m; seta2=\E[3m; %3t=\E[4m; %4t=\E[5m; %5m%9t=\n016=E[017m.

sgr0=\E[01m, smacs=N, smcup=\E[104h, smir=\E[4h,
smkw=\E[21h, smose=\E[3m, smul=\E[4m, tbc=\E[3m,

The example above is for the terminal type "screen". What we see in
the output of infamous a comma-separated list of terminal capability names or
capnames. Some of the capabilities are standalone – like the first few in the - while
others are assigned cryptic values. Standalone terminals indicate something
the terminal can do. For example, the capability "am" indicates the terminal has
automatic right. Terminal capabilities with assigned values contain strings, which
are interpreted as commands by the terminal. The values starting with "E" (
represents escape character) of control codes that cause the terminal to
perform an action as moving the cursor to a specified location, or setting the

The tput command can be used to test for a capability or to output the\assigned value. Here are some examples:

+   tput longname

This outputs the full name of the current terminal type. We can specify another terminal
type by including the -t option. Here, we will ask for the full name of the terminal
named "screen:

+   tput -t screen fullname

We can inquire values from the terminal database, like the number of supported characters
 the number of columns in the current terminal:

+   tput colors
tput cols

We can test for particular capability. For example, if the current terminal supports
"bce" (background color erase - meaning that clearing or erasing text will be done using
the currently defined background color): we

+   tput be echo "True"

We can send instructions to the terminal. For example, to move the cursor to the position
20 characters to the right and 5 rows down:

+   tput cup 5 20

# tput