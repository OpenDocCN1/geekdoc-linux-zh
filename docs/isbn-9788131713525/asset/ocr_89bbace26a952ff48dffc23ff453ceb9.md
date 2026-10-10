```
WM32   0x80002040   0             ; STCR - UART Mode
WM32   0x80002000   0x13          ; Write MR1 (default after reset)
                                      ; 8-bit, no parity
WM32   0x80002000   0x07          ; Write MR2 (after MR1) (one stop bit)
WM32   0x80002018   0x0           ; Counter/Timer Upper Reg (115.2KB)
WM32   0x8000201c   0x12          ; Counter/Timer Lower Reg (divider = 18)

; Reset and enable serial port Rx/Tx
WM32   0x80002008   0x20
WM32   0x80002008   0x30
WM32   0x80002008   0x05

; define maximal transfer size
TSZ4   0x80000000   0x80003FFF   ; internal registers

; define the valid memory map
MMAP   0x00000000   0x07ffffff   ; Memory range for SDRAM
MMAP   0xF8000000   0x3ffffff    ; ROM space
MMAP   0xE0000000   0xE000eFFF   ; PowerPC logic
MMAP   0x80000000   0x8fffffff   ; Default MBAR
MMAP   0xC0000000   0XCfffFFFF   ; Linux Kernel
```

```
[TARGET]
CPUType    5200          ; the CPU type
JTAGClock  0             ; use 16 MHz JTAG clock
WORKSPACE  0x80008000    ; workspace for fast download
Wakeup     1000          ; give reset time to complete
Startup    reset
Memdelay   -2000         ; additional memory access delay
BootAddr   0xffe00100
RegList    All
DebugMode  Soft ; or hard
PowerUp    1000
WakeUp     500
MMU        XLAT
PTBase     0x000000f0
```

```
[HOST]
IP       192.168.1.9
Format   elf
Load     manual          ; load code manual or auto after reset
Prompt   uei>
```

```
[FLASH]
ChipType  AM29BX16      ; Flash type (AM29F | AM29BX8 | AM29BX16 | I28BX8 | I28BX16)
ChipSize  0x00400000    ; The size of one flash chip in bytes
Buswidth  16            ; The width of the flash memory bus in bits (8 | 16 | 32)
```