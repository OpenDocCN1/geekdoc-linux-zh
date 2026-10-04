# 14.1.5 MIPS

指令清单14.9 Non-optimizing GCC 4.4.5 (IDA)

```
main:

; IDA is not aware of variable names in local stack
; We give them names manually:
i		= -0x10
saved_FP	= -8
saved_RA	= -4

; function prologue:
	addiu	$sp, -0x28
	sw	$ra, 0x28+saved_RA($sp)
	sw	$fp, 0x28+saved_FP($sp)
	move
; initialize counter at 2 and store this value in local stack
	li	$v0, 2
	sw	$v0, 0x28($fp)
; pseudoinstruction. "BEQ $ZERO, $ZERO, loc_9C" in fact:
		loc_9C
	or	$at, $zero ; branch delay slot, NOP
```

```
loc_80:		# CODE XREF:main+48
; load counter value from local stack and call printing_function():
	lw	$a0, 0x28($fp)
	jal	printing_function
	or	$at, $zero ; branch delay slot, NOP
; load counter, increment it; store back:
	lw	$v0, 0x28+($fp)
	or	$at, $zero ; NOP
	addiu	$v0, 1
	sw	$v0, 0x28+($fp)
```

```
loc_9C:		# CODE XREF:main+18
; check counter, is it 10?
	lw	$v0, 0x28($fp)
	or	$at, $zero ; NOP
	slti	$v0, 0xA
; if it is less than 10, jump to loc_80 (loop begin):
	bnez	$v0, loc_80
	or	$at, $zero ; branch delay slot, NOP
; finishing, return 0:
	move	$v0, $zero
; function epilogue:
	move	$sp, $fp
	lw	$ra, 0x28+saved_RA($sp)
	lw	$fp, 0x28+saved_FP($sp)
	addiu	$sp, 0x28
	jr	$ra
	or	$at, $zero ; branch delay slot, NOP
```