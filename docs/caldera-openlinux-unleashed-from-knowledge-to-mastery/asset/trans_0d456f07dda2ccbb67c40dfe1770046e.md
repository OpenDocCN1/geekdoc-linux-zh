

## check_relay -- 在 SMTP 启动时检查主机名/地址

SLocal_check_relay
Check_relay
RS$        $: $1 $; $>"Local_check_relay" $1
RS$ $*  $* $; $#3
RS$ $; $*  $0 $>"Basic_check_relay" $1 $; $2

## check_mail -- 检查 SMTP 'MAIL FROM:' 命令参数

SLocal_check_mail
Check_mail
RS$        $: $1 $; $>"Local_check_mail" $1
RS$ $*  $#5$  $:$2
RS$ $; $*  $0 $>"Basic_check_mail" $1

## Basic_check_mail

# 检查延迟投递模式
RS$        $: <$(deliveryMode)> $1
R< d > $*  $0 deferred
R< $* > $*       $: $2

R<>          $0 <OK>
RS$        $: $> $>Parse@ $3 $1    将域名规范化
R<?> $* < @ $* >     .- <?> $1 < @ $2 > $3    去除尾部点号
# 处理非 DNS 主机名（ *bitnet, * decnet, * uucp, 等）
R<?> $* < * $-P > $* $: <OK> $1 < @ $2 $3 > $4
R<?> $* < @ $* > $* $: .-7 $(resolve $2 $; $2 <PERM> $) > $1 < @ $2 > $3

R<?> $* <S-> $* @ < $> > $*
$: <$2> $3 < @ $4 > $5

# 处理地址中 @localhost 的情况
R<$> $* < @localhost $* : S: < ? $&(client_name) > < $1> $2 < @localhost.\$m >
R<$> $* < @localhost.$m >
$: < ? $&(client_name) > < $1> $2 < @localhost.\$m >
R<$> $* < @localhost.UUCP >
$: < ? $&(client_name) > < $1> $2 < @localhost.UUCP >
R<?> $S-=w> $S+> $*
R<?> $*> <$3> $*
$Erroror $0 5.5.4 $ '553 Real domain name required'
R<?> <$S> $*
$: <$1> $2

# 处理地址中没有 @domain 的情况
R<> $*
$: < ? $&(client_name) > $1
R<> $*
$ <OK> : ,,,local unqualified ok
R<?> $*> $*
$Erroror $0 5.5.4 $ '553 Domain name required'
...remote is not

# 检查结果
R<> $*
$ <OK>
R<> $*
$ <OK>
R<TEMP> $*
$Erroror $0 4.1.8 $ '451 Sender domain must resolve'
R<PERM> $*
$Erroror $0 5.1.8 $ '501 Sender domain must exist'

## check_rctp -- 检查 SMTP "RCPT TO:" 命令参数

Slocal_check_rctp
Scheck_rctp
RS*
$ $1 $* >local_check_rctp' $1
RS+ $ $S*
$ <$2
RS+ $ S*
$ $0 $'Basic_check_rctp' $1

## Basic_check_rctp

# 检查延迟投递模式
RS*
$ : < $&(deliveryMode) > $1
R< d > $*
$0 deferred
R< $* > $*
$ : $2

RS*
$ $>ParseRecipient $1 去除可中继的主机

# 任何在本地终止的都是合法的
RS+ < @ $S=\$ >
$0 OK
RS+ < @ $* =R $* >
$0 OK

# 检查本地用户（即无限定地址）
RS*
$ : <$2> $1
R<?> $* > < $S > $*
$ : <$REMOTE> $1 < @ $2 >
# 本地用户是合法的
R<?> $*
$0 OK

19 邮件服务

R<$+> $*                $: $2

# 任何源自本地的是合法的
RS*                       $: <?> $&(client_name)
# 检查是否为括号包裹的 IP 地址（正向查找 != 反向查找）
R<-> [S*]               $: <BAD> [$1]
# 传递给名称服务器以将主机名规范化
R<?> $* $-P             $: <?> $1 $2 $
R<$+> $*                $: $2
RS* .                   $1      去除尾部点号
R$0                     $0 OK
RS=                     $0 OK
RS* $-R                 $0 OK

# 检查 IP 地址
RS*                       S: $&(client_addr)
R$0                     $0 OK      源自本地
R0                      $0 OK      源自本地
R=R $*                  $0 OK      中继 IP 地址
RS*                     $: [ $1 ]    加上括号...
RS=                     $0 OK      ... 并检查是否为本地

# 其他任何情况均为无效
RS*                     $error $ 5.7.1 $: "550 Relaying denied"

#
##########################################
##########################################

####        邮件器定义
#####
##########################################
##########################################

######################
### 本地和程序邮件器规范 ###
################################################

#####    @(#)local.m4   8.30 (Berkeley) 6/30/90  #####

Local,    P=/usr/libexec/sendmail/mail.local, F=lsDFMAw:/;@qSx$fmnz9,
S=10/30, R=20/40,
T=DNS/RFC822/X-Unix,
A=mail_local -l
Mprog,    P=/bin/sh, T=lsDFMQueue9, S=10/30, R=20/40, D=$z:/,
T=X-Unix,
A=sh -c $u

#
# 信封发件人重写

Mail Services
445
第 19 章
19
MAIL SERVICES

#
S10
R<@>		$&		错误发送至 mailer-daemon
RE <@ $*> 	$&		临时绕过 Sun 的瑕疵
RS+	$: $>50 $1	如有需要添加本地域名
RS*	$: $>94 $1	执行伪装（masquerading）

#
# 信封收件人重写
#
S20
RS+ < @ $* >	$: $1		去除主机部分

#
# 头文件发件人重写
#
S30
R<@>		$&		错误发送至 mailer-daemon
RE <@ $*> 	$&		临时绕过 Sun 的瑕疵
RS+	$: $>50 $1	如有需要添加本地域名
RS*	$: $>93 $1	执行伪装（masquerading）

#
# 头文件收件人重写
#
S40
RS+	$:	$>50 $1	如有需要添加本地域名

#
# 添加本地域名名的公共代码（仅在 always-add-domain 时）
#
S50
RS+ < @ $* >*$	$@ $1 < @ $2 > $3	已完全限定
RS*	$@ $1 < @ *LOCAL* >	添加本地限定

##########################
### SMTP 邮件器规范 ###
##########################

#### @(#)smtp.m4	8.38 (Berkeley) 5/19/98 ####

Msmtp,	P=[IPC], F=mDFMuX, S=11/31, R=21, E=\r\n, L=990,
	T=DNS/RFC822/SMTP,
	A=IPC $
Mesmtp,	P=[IPC], F=mDFMuXa, S=11/31, R=21, E=\r\n, L=990,
	T=DNS/RFC822/SMTP,
	A=IPC $
Msmtp8,	P=[IPC], F=mDFMuX8, S=11/31, R=21, E=\r\n, L=990,
	T=DNS/RFC822/SMTP,
	A=IPC $
Mrelay,	P=[IPC], F=mDFMuXa8, S=11/31, R=61, E=\r\n, L=2040,
T=DNS/RFC822/SMTP,
A=IPC $h

#
#  信封发件人重写
#
S11
RS+             S: >$1 $1             发件人/收件人公共部分
R$* ; , ; <@>   $0                     列表；特殊情况
RS+             S: >$1 $1             限定无限定名称
RS+             S: >$4 $1             执行伪装（masquerading）

#
#  信封收件人重写 --
#  如果不是对收件人进行伪装，则也包括头文件收件人
#
S21
RS+             S: >$1 $1             发件人/收件人公共部分
RS+             S: >$1 $1             限定无限定名称

#
#  头文件发件人和伪装头文件收件人重写
#
S31
RS+             S: >$1 $1             发件人/收件人公共部分
R:; <@>         $0                     列表；特殊情况

# 执行特殊的头文件重写
RS* <@> S*      $0 $1 <@> $2          通过空主机
R< @ S* > S*    $0 < @ $1 > $2        通过路由地址
RS+             S: >$1 $1             限定无限定名称
RS+             S: >$3 $1             执行伪装（masquerading）

#
#  将伪域名地址转换为真实域名地址
#
S51

# 通过 <route-addr>
R< @ S* > S*    $0 < @ $1 > $2        解析 <route-addr>

# 输出伪域名为 user@fake@relay

# 执行 UUCP 启发式规则；注意这些规则与 UUCP 邮件器共享
RS+ < @ $+ .UUCP. >     S: < $2 ! > $1       转换为 UUCP 形式
RS+ < @ S* > S*         $0 $1 < @ $2 > $3     非 UUCP 形式

# 保持这些为 .UUCP 形式以避免进一步篡改

R< $S$ ! > S- 1 $+   $0 $2 < $0 $1 .UUCP. >
R< $S$ ! > S-.$*$ S-   $0 $3 < $0 $1,$2 >
R< $S$ ! > S+   $0 $1 < $0 $S$ .UUCP. >
R< $S+ ! > S+   $1 S$ ! $2 < $0 $>      使用 UUCP_RELAY
RS+ < $0 $* : S+ >  $0 $1 < $0 $3 >      去除 mailer: 部分
RS+ < $0 >  S: $1 < @ .LOCAL* >          如果没有 UUCP_RELAY

*

# 公共发件人和伪装收件人重写

@

$G1

RS+ < $0 $* > S+  $0 $1 < $0 $2 > $3   已完全限定
RS+  $0 $1 < @ .LOCAL* >  添加本地限定

*

# 中继邮件器头文件伪装收件人重写

@

$71

RS+   S: $>G1 S$ 1
RS+   S: $>G3 $S1

###############################
##  UUCP 邮件器规范  ###
##################################

#### @(#)uucp.m4 8.30 (Berkeley) 5/19/98 ####

#

# UUCP 邮件器有无种变化。这真的
# 非常荒谬。
#

# 旧 UUCP 邮件器（两个名称）
Muucp,    P=/usr/bin/uux, F=DFMhuudd, S=12, R=22/42, M=100000,
          T=X-UUCP/X-UUCP/X-Unix,
          A=uux -r -asg -gC $hirsmail ($0)
Muucp-old,  P=/usr/bin/uux, F=DFMhuudd, S=12, R=22/42, M=100000,
          T=X-UUCP/X-UUCP/X-Unix,
          A=uux -r -asg -gC $hirsmail ($0)

.# 智能 UUCP 邮件器（处理多个地址）[两个名称]

Muucp,  P=/usr/bin/uux, F=DFMhuudd, S=12, R=22/42, M=100000,
       T=X-UUCP/X-UUCP/X-Unix,
       A=uux -r -asg -gC $hirsmail ($0)

Muucp-new,  P=/usr/bin/uux, F=DFMhuudd, S=12, R=22/42, M=100000,
       T=X-UUCP/X-UUCP/X-Unix,

