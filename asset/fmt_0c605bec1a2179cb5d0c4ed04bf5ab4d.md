
# 系统启动配置脚本

## 时钟配置转换

```bash
# convert old style clock config to new values
if [ "$CLOCKMODE" = "GMT" ]; then
  UTC=true
elif [ "$CLOCKMODE" = "ARC" ]; then
  ARC=true
fi
```

```bash
CLOCKDEF=""
CLOCKFLAGS="--hctosys"
```

```bash
case "$UTC" in
  yes|true)
    CLOCKFLAGS="$CLOCKFLAGS -u"
    CLOCKDEF="$CLOCKDEF (utc)"
  ;;
  no|false)
    CLOCKFLAGS="$CLOCKFLAGS --localtime"
    CLOCKDEF="$CLOCKDEF (localtime)"
esac
```

```bash
case "$ARC" in
  yes|true)
    CLOCKFLAGS="$CLOCKFLAGS -A"
    CLOCKDEF="$CLOCKDEF (arc)"
  ;;
esac
```

```bash
case "$SRM" in
  yes|true)
    CLOCKFLAGS="$CLOCKFLAGS -S"
    CLOCKDEF="$CLOCKDEF (srm)"
  ;;
esac
```

```bash
/sbin/hwclock $CLOCKFLAGS
```

```bash
action "$Setting clock $CLOCKDEF: `date`" date
```

```bash
if [ "/sbin/consoletype" = "vt" ]; then
  # Load keymap
  if [ -x /bin/loadkeys ]; then
```

## 键盘配置

```bash
KEYTABLE=
KEYMAP=
if [ -f /etc/sysconfig/console/default.kmap ]; then
  KEYMAP=/etc/sysconfig/console/default.kmap
else
  if [ -f /etc/sysconfig/keyboard ]; then
    /etc/sysconfig/keyboard
  fi
fi
```

```bash
if [ -n "$KEYTABLE" -a -d /usr/lib/kbd/keymaps -o -d /lib/kbd/keymaps ]; then
  KEYMAP=$KEYTABLE
fi
```

```bash
if [ -n "$KEYMAP" ]; then
  # Since this takes in input/output from stdin/out, we can't use initlog
  if [ -n "$KEYTABLE" ]; then
    echo -n "Loading default keymap ($KEYMAP):"
  else
    echo -n "Loading default keymap: "
  fi
  loadkeys $KEYMAP < /dev/tty0 > /dev/tty0 2>/dev/null && success "Loading default keymap" || fail "Loading default keymap"
  echo
fi
```

## 系统字体加载

```bash
# Load system font
if [ -x /sbin/setsysfont ]; then
  [ -f /etc/sysconfig/i18n ] && . /etc/sysconfig/i18n
  if [ -f /etc/sysconfig/console/ -o \
    -f /usr/lib/kbd/consolefonts/$SYSFONT.psf -o \
    -f /etc/sysconfig/console/$SYSFONT.gz -o \
    -f /usr/lib/kbd/consolefonts/$SYSFONT.gz -o \
    -f /usr/lib/kbd/consolefonts/$SYSFONT.psf ]; then
    action "Setting default font ($SYSFONT):" /sbin/setsysfont
  fi
fi
```

## 交换分区激活

```bash
# Start up swapping.
action "Activating swap partitions: " swapon -a -e
```

## 主机名设置

```bash
if [ -f /fastboot ] || grep -iq "fastboot" /proc/cmdline 2>/dev/null ; then
  fastboot=yes
else
  fastboot=no
fi
```

## fsck 选项配置

```bash
if [ -f /fsckoptions ]; then
  fsckoptions=`cat /fsckoptions`
else
  fsckoptions=
fi
```

```bash
if [ -f /forcefsck ]; then
  fsckoptions="-f $fsckoptions"
fi
```

```bash
if [ "$BOOTUP" != "serial" ]; then
  fsckoptions="-C $fsckoptions"
else
  fsckoptions="-V $fsckoptions"
fi
```

## 根文件系统检查

```bash
ROOTFSYPE=`grep " " /proc/mounts | awk '{ print $2 }'`
if [ -z "$fastboot" -a "$ROOTFSYPE" != "nfs" ]; then
  STRING="Checking root system"
  echo $STRING
  initlog -c $fsckoptions
  rc=$?
  if [ "$rc" = "0" ]; then
    success "$STRING"
  elif [ "$rc" = "1" ]; then
    passed "$STRING"
  fi
  # return of 2 or higher means serious problems.
  if [ $rc -gt 1 ]; then
    failure "$STRING"
    echo "An error occurred during file check."
    echo "Dropping to a shell; the system will reboot when you leave the shell."
    PSI="$(Repair filesystem)"
    exit
  fi
fi
```

```bash
echo "Unmounting systems"
umount -a
mount -n -o remount,ro /
echo "Automatic reboot in progress."
reboot -f
elif [ "$rc" = "1" ]; then
  RUN_FSCHECK=1
fi
```

## PNP 设备配置

```bash
# check for arguments
if grep -iq np /proc/cmdline >/dev/null ; then
  PNP=
else
  PNP=yes
fi
```

```bash
# set up pnp
if [ -x /sbin/isapnp -f /etc/isapnp.conf -f /proc/isapnp ]; then
  if [ -n "$PNP" ]; then
    action "Setting PNP devices: " /sbin/isapnp /etc/isapnp.conf
  else
    action "Setting PNP configuration at request: " /bin/true
  fi
fi
```

## 根文件系统重新挂载

```bash
# Remount the root filesystem read-write.
state=$(awk '/^\dev\/root/ { print $4 }' /proc/mounts)
[ "$state" = "/" ] && action "Remounting root filesystem in read-write mode: " mount -n -o remount,rw /
```

## LVM 初始化

```bash
# LVM initialization
if [ -e /proc/lvm -f /lvtab ]; then
  action "Setting up LVM: " /sbin/vgscan && /sbin/vgchange -a
fi
```

## mtab 清理

```bash
# Clear mtab
> /etc/mtab
```

```bash
# Remove stale backups
rm -f /etc/mtab*
```

```bash
# Enter root, /proc and (potentially) /proc/bus/usb and devfs into mtab.
mount -f /
mount -f /proc
[ -f /proc/bus/usb/devices ] && mount -t devfs /proc/bus/usb
[ -e /dev ] && mount -t devfs /dev
```

## 硬盘优化配置

```bash
# Turn on harddisk optimization for all disks
# There is only one file /etc/sysconfig/harddisks
# after installing hdparm-RPM. If you need different hdparm parameters
# for each of your disks, copy /etc/sysconfig/harddisks to
# /etc/sysconfig/hardda (hdb, hdc...) and modify it.
# each disk with no special parameters will use the defaults.
```

```bash
disk[0]-d; disk[1]-hda; disk[2]-hdb; disk[3]-hdc;
disk[4]-hdd; disk[5]-hde; disk[6]-hdf; disk[7]-hdg; disk[8]-hdhi;
```

```bash
if [ -x /sbin/hdparm ]; then
  for device in 0 1 2 3 4 5 6 7 8; do
    unset MULTIPLE_IO USE_DMA IDE_32BIT LOOKAHEAD EXTRA_PARMS
    if [ -f /etc/sysconfig/harddisk$disk[device] ]; then
      /etc/sysconfig/harddisk$disk[device]
    fi
    HDFAGS[$device]=
    if [ -n "MULTIPLE_IO" ] && [ "MULTIPLE_IO" = "0" ]; then
      HDFAGS[$device]="-q -m$MULTIPLE_IO"
    fi
    if [ -n "USE_DMA" ] && [ "USE_DMA" = "0" ]; then
      HDFAGS[$device]="${HDFAGS[$device]}" -q$USE_DMA"
    fi
    if [ -n "IDE_32BIT" ]; then
      HDFAGS[$device]="${HDFAGS[$device]}" -c$IDE_32BIT"
    fi
    if [ -n "LOOKAHEAD" ]; then
      HDFAGS[$device]="${HDFAGS[$device]}" -a$LOOKAHEAD"
    fi
    if [ -n "EXTRA_PARMS" ]; then
      HDFAGS[$device]="${HDFAGS[$device]} $EXTRA_PARMS"
    fi
    if [ -n "$HDFAGS[$device]" ]; then
      action "Setting hard drive parameters for /dev/$disk[device]:" /sbin/hdparm $HDFAGS[$device] /dev/$disk[device]
    fi
    if -e /proc/ide/$disk[device]/media ]; then
      hdmedia=$(cat /proc/ide/$disk[device]/media)
      if [ "$hdmedia" = "disk" ]; then
        action "Setting hard drive parameters for /dev/$disk[device]:" /sbin/hdparm $HDFAGS[$device] /dev/$disk[device]
      fi
    fi
  done
fi
```

## 模块依赖处理

```bash
if [ -n "mver" ]; then
  ls /lib/modules/$mver /lib/modules/default
fi
```

```bash
if [ -L /lib/modules/default ]; then
  INITLOG_ARGS= action "Finding module dependencies: " depmod -A default
else
  INITLOG_ARGS= action "Finding module dependencies: " depmod -A
fi
```

## ISA PNP 声音配置

```bash
# 如果需要，调整 inapnp 设置。
if [ -n "SPNP" -a -f /proc/isapnp -a -x /sbin/sndconfig ]; then
  sbin/sndconfig -mungenp >/dev/null 2>&1
fi
```

## 声音模块加载

```bash
# 如果 DMA 缓冲区持续，则加载声音模块
if grep -q "options dmambuf=1" /etc/modules.conf 2>/dev/null ; then
  RETURN=0
  alias="/sbin/modprobe -c | grep -s "$alias[[:space:]]+sound[[:space:]] \\ 
  +=" | awk '{ print $3 }'
  if [ -n "$alias" -a "$alias" != "" ]; then
    action "Loading sound module ($alias): " modprobe $alias
    RETURN=$0
  fi
fi
```

## 混音器设置加载

```bash
# 加载混声器设置
if grep -q "/sparcaudio/sound/" /proc/devices 2>/dev/null ; then
  if [ $RETURN -eq 0 -a -f /etc/.auximrc -a -x /bin/auxmixer-minimal ]; then
    action "Loading mixer settings: " /bin/auxmixer-minimal -f /etc/.auximrc -L
  fi
fi
```

## 内核模块代理配置

```bash
if [ -f /proc/sys/kernel/modprobe ]; then
  if [ -n "$USEMODULES" ]; then
    sysctl -w kernel.modprobe=/sbin/modprobe >/dev/null 2>&1
    sysctl -w kernel.hotplug=/sbin/hotplug >/dev/null 2>&1
  else
    # 我们以前曾将其设置为 NULL，但那会导致“执行失败”的错误信息
    sysctl -w kernel.modprobe="bin/true" >/dev/null 2>&1
    sysctl -w kernel.hotplug="bin/true" >/dev/null 2>&1
  fi
fi
```

## 模块加载兼容性

```bash
# 加载模块（为了与 VAR 向后兼容）
if [ -f /etc/rc.modules ]; then
  /etc/rc.modules
fi
```

## RAID 设备启动

```bash
# 添加 raid 设备
if [ ! -f /proc/mdstat ]; then
  modprobe >/dev/null 2>&1
fi

if [ -f /proc/mdstat -a f /etc/raidtab ]; then
  echo -n "Starting up RAID devices: "
  rc=0
  for i in `grep "^raiddev" /etc/raidtab | awk '{print $2}'`
  do
    RAIDDEV=`basename $i`
    RAIDSTAT=`grep "$$RAIDDEV : active" /proc/mdstat`
    if [ -z "$RAIDSTAT" ]; then
      # 先尝试 raidstart...如果失败了
      # 则回退到 raiddadd, raidrun。如果这些
      # 也失败了，那么我们将进入 shell
      RESULT=-1
```
