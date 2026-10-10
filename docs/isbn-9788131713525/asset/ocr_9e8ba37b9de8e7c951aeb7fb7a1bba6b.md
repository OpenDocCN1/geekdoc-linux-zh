```
; bit 16: Multiplex or non-mux'ed (0x0 = non-muxed)
; bit 17: reserved (Reset value = 0x1, keep it)
; bit 18: Ack Active (0x0)
; bit 19: CE (Enable) 0x1
; bits 20-21: Address Size (0x11 = 25/6 bits)
; bits 22:23: Data size field (0x01 = 16-bits)
; bits 24:25: Bank bits (0x00)
; bits 26-27: WaitType (0x11)
; bits 28: Write Swap (0x0 = no swap)
; bits 29: Read Swap (0x0 = no swap)
; bit 30: Write Only (0x0 = read enable)
; bit 31: Read Only (0x0 = write enable)
```

```
; CS2 Logic Registers
WM32 0x80000014 0x0000e00e
WM32 0x80000018 0x0000efff

; LEDs:
; LED1 - bits 0-7
; LED2 - bits 8-15
; LED3 - bits 16-23
; LED4 - bits 24-31
; off = 0x01
; on = 0x02
; mm 0xe00e2030 0x02020202 1 (all on)
; mm 0xe00e2030 0x01020102 1 (2, on off)
```

```
WM32 0x8000308 0x0045b30 ; CS2 Configuration Register
; bits 0-7: WaitP (try 0xff)
; bits 8-15: WaitX (try 0xff)
; bit 16: Multiplex or non-mux'ed (0x0 = non-muxed)
; bit 17: reserved (Reset value = 0x1, keep it)
; bit 18: Ack Active (0x0)
; bit 19: CE (Enable) 0x1
; bits 20-21: Address Size (0x10 = 24 bits)
; bits 22:23: Data size field (0x11 = 32-bits)
; bits 24:25: Bank bits (0x00)
; bits 26-27: WaitType (0x11)
; bits 28: Write Swap (0x0 = no swap)
; bits 29: Read Swap (0x0 = no swap)
; bit 30: Write Only (0x0 = read enable)
; bit 31: Read Only (0x0 = write enable)
```

```
WM32 0x80000318 0x01000000 ; Master LFC Enable

; init SDRAM controller
; For the UEI PPC 5200 Board,
; Micron 46V32M16-7SE (8 MEG x 16 x 4 banks)
```