
## 目录列表示例

```
apps/          layout         sys@
archives/      lib@           tftpboot/
bin@           lost+found/    tmp/
boot           mnt/           usr/
cdrom/         net/           utilities/
chess/         news/          var/
dev/           nntpserver     vmunix*
etc/           pcfs/
```

## `ls -F` 输出

```
% ls -F

Archives/      Mail/          RUMORS.18Sept  mailing.lists
InfoWorld/     News/          bin/           newlists
LISTS          OWL/           iecc.list      src/

%
```

## `ls -aF` 输出

```
% ls -aF

./          .gopherrc      .oldnewsrc     .sig           RUMORS.18Sep
../         .history*      .plan          Archives/       bin/
.Agenda     .info          .pnewsexpert   InfoWorld/      iecc.list
.aconfigrc  .letter        .report        LISTS           mail.lists
.article    .login         .rm-timestamp  Mail/           newlists
.cshrc      .mailrc        .rnlast        News/           src/
.elm/       .newsrc        .rnsoft        OWL/

%
```

## `env` 输出

```
% env

HOME=/home/taylor
SHELL=/bin/csh
TERM=vt100
PATH=/home/taylor/bin:/bin:/usr/bin:/usr/ucb:/usr/local/bin:
→/usr/unsup/bin:.
MAIL=/usr/spool/mail/taylor
LOGNAME=taylor
TZ=EST5

%
```

## `echo $PATH` 与 `echo $HOME`

```
% echo $PATH
/home/taylor/bin:/bin:/usr/bin:/usr/ucb:/usr/local/bin:/usr/unsup/
→ bin:.
% echo $HOME
/home/taylor

%
```

## `cd` 错误示例

```
% cd /taylor
/taylor: No such file or directory

%
```

## `ls -C -F` 输出

```
% ls -C -F

armstrong/  christine/  guest/  laura/  matthew m/  shane/
bruce/  david/  higgins/  mac/  rank/  taylor/
cedric/  green/  kane/  mark/  shalini/  vicki/

%
```

## 隐藏文件示例

```
.test  hide-me  ,test  .cshrc
../  .dot.  dot  .HiMom

.cshrc    .rnsoft    .exrc    .print
.tmp334   .excel/    .letter   .vi-expert

/Personnel/Taylor,D.
/home/taylor/business/California
.../...
Recipe:Gazpacho
```

## `ls` 输出

```
% ls

Archives      Mail          RUMORS.18Sept  mailing.lists
InfoWorld     News          bin            newels
LISTS         OWL           iecc.list      src

%
```

## `ls -s` 输出

```
% ls -s

total 563

    1 Archives      1 Mail      5 RUMORS.18Sept  280 mailing.lists
    1 InfoWorld     1 News      1 bin           2 newels
261 LISTS         1 OWL       4 iecc.list      1 src

%
```

## `ls -s LISTS iecc.list newels`

```
% ls -s LISTS iecc.list newels

261 LISTS      4 iecc.list    2 newels

%
```

## `ls -a` 输出

```
% ls -a

.           gopherrc    .oldnewsrc  .sig        RUMORS.18Sept
..          .history    .plan       Archives    bin
.Agenda     .info       .pnewsexpert InfoWorld   iecc.list
.aconfigrc  .letter     .report     LISTS       mailing.lists
.article    .login      .rm-timestamp Mail        newels
.cshrc      .mailrc     .rnlast     News        src
.elm        .newsrc     .rnsoft     OWL

%
```

## `ls -F` 重复示例

```
% ls -F

Archives/      Mail/          RUMORS.18Sept  mailing.lists
InfoWorld@     News/          bin/           newels
LISTS          OWL/           iecc.list      src/

%
```

## `ls -s -F` 输出

```
% ls -s -F

total 403

    1 Archives/    1 Mail/      5 RUMORS.18Sept  280 mailing.lists
    1 InfoWorld/   1 News/      1 bin/          2 newels
  261 LISTS       1 OWL/       4 iecc.list      1 src/

%
```

## `ls -F /usr` 输出

```
% ls -F /usr

5bin/      diag/      lddrv/     share/     ucbinclude@
5include/  dict/      lib/       source/    ucblib@
5lib/      etc/       local/     spool@     xpg2bin/
acc/       export/    lost+found/ src@       xpg2include/
acctlog*  games/     man@       stand@     xpg2lib/
adm@      hack/      mdec@      sys@
bin/      hosts/     old/       system/
boot@     include/   pub@       tmp@
demo/     kvm/       sccs/      ucb/
```
