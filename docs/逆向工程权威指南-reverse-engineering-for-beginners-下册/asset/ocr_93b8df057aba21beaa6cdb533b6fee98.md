# 由于源程序很小的缘故，GCC会全局指针在64KB可视空间进行表查

# 指令18.29 Optimizing GCC 4.4.5 (IDA)

```
insert:
; $a0=x
; $a1=y
; $a2=z
; $a3=value
	sll	$v0, $a0, 5
	$v0 = $a0<<5 = x*32
	sll	$a0, 3
	$a0 = $a0<<3 = x*8
	addu	$a0, $v0
	$a0 = $a0+$v0 = x*8+x*32 = x*40
	sll	$v1, $a1, 5
	$v1 = $a1<<5 = y*32
	sll	$v0, $a0, 4
	$v0 = $a0<<4 = x*40*16 = x*640
	sll	$a1, 1
	$a1 = $a1<<1 = y*2
	sub	$a1, $v1, $a1
	$a1 = $v1-$a1 = y*32-y2 = y*30
	sub	$a0, $v0, $a0
	$a0 = $v0-$a0 = x*640-x*40 = x*600
	addu	$gp, __gnu_local_gp
	$a0 = $a1+$a0 = y*30+x*600
	addu	$a0, $a2
	$a0 = $a0+$a2 = y*30+x*600+z
	load address of table:
	lw	$v0, (a & 0xFFFF)($gp)
	multiply index by 4 to seek array element:
	sll	$a0, 2
	sum up multiplied index and table address:
	addu	$a0, $v0, $a0
	store value into table and return:
	jr	$Ra
	sw	$a3, 0 ($a0)

.comm a:0x1770
```

# 18. 6. 4 更多案例

计算机的显示屏幕是一个二维显示空间，但是内存是一个一维的线性数组。