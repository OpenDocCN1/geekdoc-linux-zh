
# (@arrays,v1.0) (Wayne.Thompson) 05/02/93

## 描述
此包包含模拟关联数组的函数。
键限于长度、下划线和点。

## 变量
`_array_size_<array>`
`_array_keys_<array>`
`_array-<array>-<key>`
`_array_filename`
`_array_name`
`_array_key`
`_array_keys`
`_array_cell`

## 使用
`setarray array key [value ...]`
`getarray array key`
`unsetarray key [...]`
`keys array`
`size array`
`defined array [key]`
`dumarray pathname [array ...]`

## 依赖
数组名和键组合成字符串作为参数评估。

### FUNCTION: setarray =======================

## 函数
(@setarray,v1.0) (Wayne.Thompson) 05/16/93

## 描述
此函数为数组元素赋值。
如果提供了多个值且键为整数，值将从初始键开始赋值给连续元素。

## 变量
`_array_size_<array>`
`_array_keys_<array>`
`_array-<array>-<key>`

## 示例脚本 505

```bash
# __array_name
# __array_key
# __array_cell
# 使用:
#    setarray array key [value ...]
#    setarray pathname
# 返回:
# 依赖:
# 错误:
setarray () {
    case $# in
        echo >&2 setarray: error: "$*"
        echo >&2 usage: setarray array '{value ...}'
        exit 1
        fi)
    if [ -f $1 ]; then
        while read __array_name __array_key __array_value
        do
            setarray $__array_name __array_key __array_value
        done < $1
    else
        echo >&2 setarray: error: $1: no such文件
        exit 1
    fi
    case $2 in
        [0-9]*)
            echo >&2 setarray: error: "$*"
            echo >&2 setarray: error: 第二参数必须是整数
            exit 1
        esac
    esac
    array_name=$1
    array_key=$2
    case $2 in
        [-].*)
            array_cell=$(echo $2 | /bin/tr '[-.]')
            shift 2
            set $__array_name $array_cell "$*"
            ;;
    esac
    if [ ${__array_size=$1+1} ]; then
        [ ${__array_size=$$$2+1} ] || (
            __array_size=$(/bin/expr $__array_size + 1)
        )
        array_keys=${__array_keys $array_key ""
    else
        __array_size=$1
        _array_keys=$1=$2
    fi
    array_$1=$2=$3
    case $# in
        2)
            shift 2
            ;
        *)
            shift 3
            ;
    esac
    while [ $# -gt 0 ];
    do
        array_key=$(/bin/expr \$array_key + 1)
        eval \
            * (${array_name}_${array_key}) | (
                _${array_size}_${array_name} += 1
                _${array_keys}_${array_name}
            )
            _${array_name}_${array_key}=\$1
            shift
    done
}
```

## 506

## 参考表与示例脚本

```bash
getarray() {
    case $# in
        echo >&2 getarray: error: "$*"
        echo >&2 usage: getarray array '{value ...}'
        exit 1
        fi)
    if [ -f $1 ]; then
        while read __array_name __array_key __array_value
        do
            setarray $__array_name __array_key __array_value
        done < $1
    else
        echo >&2 getarray: error: $1: no such文件
        exit 1
    fi
    case $2 in
        [0-9]*)
            echo >&2 getarray: error: "$*"
            echo >&2 getarray: error: 第二参数必须是整数
            exit 1
        esac
    esac
    array_name=$1
    array_key=$2
    case $2 in
        [-].*)
            array_cell=$(echo $2 | /bin/tr '[-.]')
            shift 2
            set $__array_name $array_cell "$*"
            ;;
    esac
    if [ ${__array_size=$1+1} ]; then
        [ ${__array_size=$$$2+1} ] || (
            __array_size=$(/bin/expr $__array_size + 1)
        )
        array_keys=${__array_keys $array_key ""
    else
        __array_size=$1
        _array_keys=$1=$2
    fi
    array_$1=$2=$3
    case $# in
        2)
            shift 2
            ;
        *)
            shift 3
            ;
    esac
    while [ $# -gt 0 ];
    do
        array_key=$(/bin/expr \$array_key + 1)
        eval \
            * (${array_name}_${array_key}) | (
                _${array_size}_${array_name} += 1
                _${array_keys}_${array_name}
            )
            _${array_name}_${array_key}=\$1
            shift
    done
}
```

## 示例脚本 507
done
