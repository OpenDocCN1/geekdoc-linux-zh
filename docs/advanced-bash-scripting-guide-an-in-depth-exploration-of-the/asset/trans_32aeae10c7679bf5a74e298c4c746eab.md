

# 高级 Bash 脚本指南

```bash
echo "WARNING: the rsync process did not entirely succeed.
echo "Something might be wrong."
echo "Saving an extra copy to $BACKUP_JUSTINCASE"
echo "WARNING: if this occurs regularly, a LOT of space will be consumed,"
echo "even though these are just hard-linked!"```

```bash
# 在备份目录中保存一个 readme。
# 在最近的子目录中保存另一个。
echo "在 '$hostname' 上的 $SOURCE_DIR 备份上次运行于 \$(date)" > $BACKUP_DEST_DIR/README.txt
echo "在 '$hostname' 上的 $SOURCE_DIR 此次备份备份创建于 \$(date)" > $BACKUP_DEST_DIR/backup.0/README.txt
```

```bash
# 如果不是模拟运行，则轮换备份。
[ "$DRY_RUN" != "" ]
# 检查备份磁盘是否满。
# 如果达到 90% 或 98% 则警告，我们可能会失败，因此放弃。
# （注意：我们可以计算多行）。
# 我们在之后进行测试，而不是之前，
# 这样 rsync 才可能还有机会。
DISK_FULL_PERCENT=$(/bin/df $BACKUP_DEST_DIR | tr -d "%" | awk '{print $1}' | grep -e [0-9]+)
echo "备份分区上创建的空间 "
MOUNT_POINT=$DISK_FULL_PERCENT%
if [ $DISK_FULL_PERCENT -ge 90 ]; then
	echo "WARNING: 磁盘空间已大于 90%。"
	fi
fi
```

```bash
if [ $DISK_FULL_PERCENT -ge 98 ]; then
	echo "Error: 磁盘满了！放弃。"
	if [ "$MOUNT_LATER" == "TRUE" ]; then
		# 在退出之前，如有必要卸载挂载点。
		cd; sudo unmount $MOUNT_POINT &&
		echo "再次卸载了 $MOUNT_POINT。放弃。"
	fi
	exit $S_UNMOUNTED
fi
```

```bash
# 创建一个额外的备份，放弃。
if [ -n "$BACKUP_JUSTINCASE" ]; then
	if ! /bin/cp -al $BACKUP_DEST_DIR/backup.0 \
	$BACKUP_DEST_DIR/$BACKUP_JUSTINCASE
	then
		echo "ERROR: 创建额外副本 $BACKUP_DEST_DIR/$BACKUP_JUSTINCASE 失败"
		if [ "$MOUNT_LATER" == "TRUE" ]; then
			# 在退出之前，如有必要卸载挂载点。
			cd; sudo unmount $MOUNT_POINT &&
			echo "再次卸载了 $MOUNT_POINT。放弃。"
		fi
		exit $S_UNMOUNTED
	fi
fi
```

```bash
# 月初轮换最旧的 8 个。
if [ "$MONTHSTART" == "true" ]; then
	echo -e "\n月初。移除最旧的备份：$BACKUP_DEST_DIR/backup.15"
	/bin/rm -rf $BACKUP_DEST_dir/backup.15
	echo "正在轮换每月、每周备份：$BACKUP_DEST_dir/backup.[8-14] -> $BACKUP_DEST_dir/backup.[9-15]"
	/bin/mv $BACKUP_DEST_dir/backup.14 $BACKUP_DEST_dir/backup.15
	/bin/mv $BACKUP_DEST_dir/backup.13 $BACKUP_DEST_dir/backup.14
	/bin/mv $BACKUP_DEST_dir/backup.12 $BACKUP_DEST_dir/backup.13
	/bin/mv $BACKUP_DEST_dir/backup.11 $BACKUP_DEST_dir/backup.12
	/bin/mv $BACKUP_DEST_dir/backup.10 $BACKUP_DEST_dir/backup.11
	/bin/mv $BACKUP_DEST_dir/backup.9 $BACKUP_DEST_dir/backup.10
	/bin/mv $BACKUP_DEST_dir/backup.8 $BACKUP_DEST_dir/backup.9

# 周初轮换第二旧的 4个。
elif [ "$WEEKSTART" = "true" ]; then
	echo -e "\n每周开始：\移除旧的每周备份：$BACKUP_DEST_dir/backup.12"
	/bin/rm -rf $BACKUP_DEST_dir/backup.12
	echo "正在轮换每周备份：$BACKUP_DEST_dir/backup.[8-11] -> $BACKUP_DEST_dir/backup.[9-12]"
	/bin/mv $BACKUP_DEST_dir/backup.11 $BACKUP_DEST_dir/backup.12
	/bin/mv $BACKUP_DEST_dir/backup.10 $BACKUP_DEST_dir/backup.11
	/bin/mv $BACKUP_DEST_dir/backup.9 $BACKUP_DEST_dir/backup.10
	/bin/mv $BACKUP_DEST_dir/backup.8 $BACKUP_DEST_dir/backup.9

else
	echo -e "\n最旧的每日备份：$BACKUP_DEST_dir/backup.8"
	/bin/rm -rf $BACKUP_DEST_dir/backup.8

# 每天轮换最新的 8个。
	echo "正在轮换每日备份：\n$BACKUP_DEST_dir/backup.[1-7] -> $BACKUP_DEST_dir/backup.[2-8]"
	/bin/mv $BACKUP_DEST_dir/backup.7 $BACKUP_DEST_dir/backup.8
	/bin/mv $BACKUP_DEST_dir/backup.6 $BACKUP_DEST_dir/backup.7
	/bin/mv $BACKUP_DEST_dir/backup.5 $BACKUP_DEST_dir/backup.6
	/bin/mv $BACKUP_DEST_dir/backup.4 $BACKUP_DEST_dir/backup.5
	/bin/mv $BACKUP_DEST_dir/backup.3 $BACKUP_DEST_dir/backup.4
	/bin/mv $BACKUP_DEST_dir/backup.2 $BACK_DEST_dir/backup.3
	/bin/mv $BACKUP_DEST_dir/backup.1 $BACKUP_DEST_dir/backup.2
	/bin/mv $BACKUP_DEST_dir/backup.0 $BACKUP_DEST_dir/backup.2
fi

if [ $DISK_FULL_PERCENT -ge 90 ]; then
	echo "WARNING: 磁盘空间已大于 90%。"fi
```

## 附录 A. 贡献的脚本

