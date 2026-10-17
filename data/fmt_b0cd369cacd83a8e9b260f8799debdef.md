
```bash
  print $OS    # 返回大写值
)
###################################
function check_exceptions
{
# set -x # 取消注释以调试此函数

  while read FSLIMIT
  do
    IN_FILE="N"

    # 对 NFS 进行完整性检查并移除任何 "."
    # 如果找到此项，它实际上是一个错误条目
    # 但我们将尝试解析它。只有当它是
    # NFS 跨挂载到机器上的同一个
    # 挂载点时才会生效。
    echo $FSNAME | grep '.' >/dev/null \
      && $FSNAME=$(echo $FSNAME | cut -d ':' -f2)

    # 检查空或空变量
    if [[ -z $FSLIMIT && $FSLIMIT != '' ]];
    then
      if [[ $FSNAME == $FMOUNT ]]; # 找到了！
        # 检查是否存在 "MB" 字符...设置 IN_FILE=MB
        echo $FSLIMIT | grep MB >/dev/null && IN_FILE="MB" \
          && (( FSLIMIT = $(echo $FSLIMIT | sed s/MB//) * 1024 ))
        # 检查是否存在 "*" 字符...设置 IN_FILE=PC，代表 %
        echo $FSLIMIT | grep "*" >/dev/null && IN_FILE="PC" \
          && $FSLIMIT=$(echo $FSLIMIT | sed s/\*g))

      case $IN_FILE in
        MB) # 使用剩余空间 MB 方法
          # 如果存在字符，将其转为大写
          FSLIMIT=$(echo $FSLIMIT | tr '[a-z]' '[A-Z]')
          # 如果存在 "MB"，将其移除
          FSLIMIT=$(echo $FSLIMIT | sed s/MB//g)
          # 测试块值和空值
          if [[ ! -z $FSLIMIT && $FSLIMIT != '' ]];
          then
            # 测试有效的文件系统 "MB" 限制
            if (( $FSLIMIT >= 0 && $FSLIMIT < $FSIZE ))
              then
                if (( $FSMB_FREE < $FSIZE ))
                  then
                    return 1 # 发现超出限制
                    # 使用 MB 剩余方法
                  else
                    return 3 # 发现正常
                  fi
              else
                echo "\nERROR: 无效的文件系统 MAX 为 $FSMOUNT - $FSLIMIT"
                echo "      异常文件值必须小于或"
                echo "      等于文件系统的大小"
                echo "      单位为 1024 字节\n"
              fi
          else
            echo "\nERROR: 异常文件中指定了空值"
            echo "      针对 $FSMOUNT 挂载点。\n"
          fi
          ;;
        PC) # 使用文件系统使用百分比方法
          # 如果存在 % 号，将其移除
          PC_USED=$(echo $PC_USED | sed s/\%/g)
          # 测试空和空值
          if [[ -z $FSLIMIT && $FSLIMIT != '' ]];
          then
            # 测试有效百分比，例如 100
            if (( $FSLIMIT >= 0 && $FSLIMIT <= 100 ))
              then
                if (( $PC_USED >= $FSLIMIT ))
                  then
                    return 2 # 发现超出限制
                  else
                    return 3 # 发现正常
                  fi
              else
                echo "\nERROR: 无效的文件系统 MAX 为 $FSMOUNT - $FSLIMIT"
                echo "      异常文件值必须小于或"
                echo "      等于文件系统的大小"
                echo "      单位为 1024 字节\n"
              fi
          else
            echo "\nERROR: 异常文件中指定了空值"
            echo "      针对 $FSMOUNT 挂载点。\n"
          fi
          ;;
        N) # 假设没有 $EXCEPTIONS 文件
          THISTHOST="hostname" # 本地机器的主机名
          # (此处逻辑略)
            return 1 # 默认限制
          else
            return 3 # 正常
          fi
      esac
  done
```

## 第 5 章

仔细研究列表 5.15 中的脚本，将揭示处理我们在编写 shell 脚本时遇到的不同情况的一些良好方法。这些方法总是直观而易见的！

列表 5.16 中的 `/usr/local/bin/exceptions` 文件在 yogi 上使用。

```bash

# FILE: "exceptions"

#

# 此文件用于覆盖文件系统监控脚本

# fs_mon_ALL_OS_exec.ksh 中的默认

# 触发值，但也允许覆盖使用的# 监控技术，即文件系统的最大使用率

# 和最小剩余 MB 空间。覆盖语法为

# 挂载点以及带有 "%" 或 "MB" 

# 后缀的“触发值”。

# 示例：

#

# /usr 96%

# 或者

# /usr 50MB

# 所有以 # 开头的行都会被忽略。

#

# 注意：所有条目必须带有 "MB" 或

# "%%" 作为后缀！！！否则将使用

# 脚本默认值。请勿留空格！

#

/opt 95%

// 50%

/usr 70MB

/home 50MB

```

列表 5.16 示例异常文件。

列表 5.16 应该可以工作，但它会报错。如果使用这些文件条目执行监控，将产生如下输出：

```
ERROR: Invalid filesystem MINIMUM_MB_FREE specified
for /home - 50MB -- 当前大小为 4MB.
异常值必须小于或等于
以兆字节为单位的文件系统大小
```

yogi 上的完整文件系统：

```
/dev/hd4 挂载在 / 是 51%
/dev/hd2 挂载在 /usr 剩余 57MB
/dev/hd10 挂载在 /opt 是 97%
```
