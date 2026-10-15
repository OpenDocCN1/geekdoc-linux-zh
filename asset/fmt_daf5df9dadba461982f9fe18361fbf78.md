
# 第 27 章 使用 rsync 的 Dirvish 创建快照类型备份 909

```bash
echo -e "\n\t警告: default.conf 文件已存在..重构建 default.conf? (y/n): \c"
read ANS

case ANS in
ny|Y) echo -e "\n\t正在为 $HN 创建 default.conf 配置文件"
    build_default_conf $HN $BANK $DAYS $TREE"
$IGNORE_LIST
```
```

```bash
echo -e "\n正在复制文件到: $(BANK)/$(HN)/dirvish/default.conf"
cp -f $DEFAULT_CONF $(BANK)/$(HN)/dirvish/default.conf"
echo -e "\n...按回车键继续...\c"
read ANS
*)
    break
    ;
esac
else
    echo -e "\n为 $HN 创建默认的 default.conf Dirvish 配置"
    build_default_conf $HN $(BANK) $DAYS $TREE "$IGNORE_LIST"
    echo -e "\n正在复制文件到: $(BANK)/$(HN)/dirvish/default.conf"
    cp -f $DEFAULT_CONF $(BANK)/$(HN)/dirvish/default.conf"
    echo -e "\n...按回车键继续...\c"
    read ANS
fi
;
7) clear
    echo -e "\n创建初始 DIRISH 备份"
    echo -e "\n"
    if [ ! -d $(BANK)/$(HN) ]
    then
        echo -e "\n为此备份创建存储库 HN"
        mkdir $(BANK)/$(HN)
        mkdir $(BANK)/$(HN)/dirvish
    else
        echo -e "\n$HN 的备份库已存在...继续..."
    fi
    if [ ! -r $(BANK)/$(HN)/dirvish/default.conf ]
    then
        现在我们有足够的信息来构建新的 default.conf 文件
        echo -e "为 $HN 创建默认的 default.conf Dirvish 配置"
        build_default_conf $HN $(BANK) $DAYS $TREE "$IGNORE_LIST"
        echo -e "\n正在复制文件到: $(BANK)/$(HN)/dirvish/default.conf"
        cp -f $DEFAULT_CONF $(BANK)/$(HN)/dirvish/default.conf"
        # 我们现在需要运行初始备份
        echo -e "\n现在执行初始备份吗？(y/n): \c"
        read BACK_NOW
        case BACK_NOW in
```

列表 27-24 (继续)

```bash
y|Y) echo -e "\n正在为 $HN 执行初始 Dirvish 备份..."
        /usr/local/sbin/dirvish --vault $HN --init
        RC=$?
        echo -e "\n$HN 初始备份完成，返回码为 \$RC"
        echo -e "\n按回车键继续...\c"
        read KEY
        ;
      n|N) echo -e "\n跳过初始备份..."
        echo -e "\n不要忘记运行初始 Dirvish 备份!"
        echo -e "\n如需手动运行初始备份，请输入：\n"
        echo -e "\t/usr/local/sbin/dirvish --vault $HN --init\n"
        echo -e "\n按回车键继续...\c"
        read KEY
        ;
      *) echo -e "\n无效输入..."
      esac
else
  FINISH=0
  until (( FINISH == 1 ))
do
    echo -e "\n现在执行初始备份吗？(y/n):\c"
    read BACK_NOW
    case $BACK_NOW in
      y|Y) echo -e "\n正在为 $HN 执行初始 Dirvish 备份..."
        /usr/local/sbin/dirvish --vault $HN --init
        RC=$?
        echo -e "\n$HN 初始备份完成，返回码为 \$RC"
        echo -e "\n按回车键继续...\c"
        read KEY
        FINISH=1
        ;
      n|N) echo -e "\n跳过初始备份..."
        echo -e "\n不要忘记运行初始 Dirvish 备份!"
        echo -e "\n如需手动运行初始备份，请输入：\n"
        echo -e "\t/usr/local/sbin/dirvish --vault $HN\n"
        echo -e "\n按回车键继续...\c"
        read KEY
        FINISH=1
        ;
      *) echo -e "\n无效输入..."
        sleep 2
        ;
      esac
  done
```

**列表 27-24** (继续)

```bash
esac
done
fi
continue
;
8) break
;;
esac
done
)
```

```bash
delete_backup ()
{
# 此函数用于从 Dirvish 服务器删除备份
clear # 清除屏幕
echo -e "\n\t\t从 Dirvish 备份中移除服务器\n"
echo -e "\n\t输入要从 Dirvish 备份中移除的主机： \c"
read H
BANK_LIST=$(parse_conf)
for P in $BANK_LIST
do
VAULT_ID=$(find $P -type d -name "$H")
if [[ ! -z "$VAULT_ID" ]];
then
	STOP=0
	until [[ $STOP == 1 ]];
	do
		echo -e "\n\t从 Dirvish 服务器移除存储库 $H 吗？ \c"
		read ANS
	case $ANS in
	y) echo -e "\n\t正在从 Dirvish 备份中移除 $H 的存储库...\c"
		rm -fr "$VAULT_ID"
		echo -e "\n\t存储库已移除...按回车键继续...\c"
		read KEY
		STOP=1
	n) echo -e "\n\t取消移除存储库...按回车键继续...\c"
		read KEY
		STOP=1
	;;
	*) echo -e "\n\t无效输入..."
		;;
	esac
	done
fi
done
}
```
