
## 11.4.3 Scalex 系统调用处理程序

以下是文件操作结构体中指向的函数。

**程序 11.10**

```asm
glokal scalex_interrupt
RBS equ 256; This must be a power of 2.
COMI equ 3F8H; COM1 Base I/O Address and Data Port
extern scalex_area
extern printk
extern __wake_up
;
scalex_interrupt:
; Push all the registers that get used, except EAX
   PUSH ECX
   PUSH EDX
   PUSH EBX
   PUSH ESI
   PUSH EDI

   MOV EDX, COMI + 5; Line Status Register
   IN AL, DX          ;
   TEST AL, 1         ; See if Data Has Arrived
   JZ NEAR WRD        ; No? Then Need to Write Data?

; Process Incoming Data
; MOV ESI, [scalax_area + 4]; readin component of structure
   ADD ESI, RBS + 2; Read Buffer Size + 2
   SUB ESI, [scalax_area + 8]; readout component of structure
   AND ESI, RBS - 2 ; Read Buffer Size - 2
   JZ NEAR RBF        ; Read Buffer Full

; These lines test the condition:
; readin + 1 = readout OR readin + 2 = readout (mod 2^n)
; If it is true then the circular buffer has overflowed. Note RBS = 2^n.
;
   MOV EDX, COM1      ; Data Port has zero offset.
   IN AL, DX          ; This is the data byte right here!
   MOV CL, AL         ; Keep whole byte in AL
   AND ECX, 15        ; Clear ECX and look at halves in CL

   MOV DL, [OKC + ECX]; Translate incoming half byte
   MOV EBX, [scalax_area + 28]; Get address of Read Buffer
   MOV ESI, [scalax_area + 4]; readin component of structure
   MOV [EBX + ESI], DL; Store translated byte in Read Buffer
   INC ESI            ;Increment readin
   AND ESI, RBS - 1   ;mod 2^n of course
   MOV [scalax_area+ 4], ESI
   CMP DL, 10         ; Was that a terminal signal?
   JZ NEAR QWQ        ; If so wake up the reading process.

   MOV CL, AL         ; Now do the other half byte
   SHR CL, 4
   MOV DL, [OKC + ECX]; Translate incoming half byte
   MOV [EBX + ESI], DL; Store translated byte in Read Buffer
   INC ESI            ; Increment readin
   AND ESI, RBS - 1   ; mod 2^n of course
   MOV [scalax_area + 4], ESI;
   CMP DL, 10         ; Was that a terminal signal?
   JZ NEAR QWQ        ; If so wake up the reading process.

; Process Outgoing Data
WRD:  MOV EDX, COM1 + 2; Interrupt Identification Register
   IN AL, DX
   TEST AL, 2         ; Check the Data Has Been Sent Bit
   JZ NEAR LEV        ; No? Then quit.
;
; See if the end of the write buffer has been reached.
   MOV EDI, [scalax-area + 16]; writeout component of structure
   CMP EDI, [scalax_area + 12]; written component of structure
   JZ QWW             ; If done then wake up writing process.
POL:  MOV EDX, COM1 + 5; Line Status Register
   IN AL, DX
   TEST AL, 64        ; Data Has Been Sent Bit
   JZ POL             ; Should be just a short wait
   MOV EBX, [scalax_area + 24]; Get address of Write Buffer
   MOV AL, [EBX + ESI]
   MOV EDX, COM1      ; Data Port
   OUT DX, AL         ; Here is the outgoing byte!
   INC ESI
   MOV [scalax_area + 16], ESI; writeout
JMP LEV

QWQ: ; Write Queue Wake-up
; Since __wake_up() looks like a function we should expect
; to push the arguments as shown on the next two lines.
; PUSH dword 1;TASK_INTERRUPTIBLE
   PUSH dword scalax_area + 32; Wake up
   PUSH This is the double pointer!

;
; However __wake_up() actually wants its arguments passed
; in registers EDX and EAX!
   MOV EDX, 1;TASK_INTERRUPTIBLE
   MOV EAX, scalex_area + 32; Write wait queue
   CALL __wake_up
   JMP LEV

ROW: ; Read Queue Wake-up
; Test flags component for the Read Pending Bit
   TEST dword [scalex_area], 8
   JZ NEAR LEV        ; No? False alarm, just quit.
   MOV EDX, 1;TASK_INTERRUPTIBLE
   MOV EAX, scalex_area + 28; Read wait queue
   CALL __wake_up
   JMP LEV

RBF: ; Read Buffer Full
   PUSH dword OVR ; Overflow
   CALL printk
   ADD ESP, 4
   JMP LEV

; Error message:
OVR: db "Read buffer overflow!",0AH,0
;
; Half-byte to Byte Translation table:
CKC: db "0123456789AB-",0AH,"F"

LEV:
   POP EDI
   POP ESI
   POP EBX
   POP EDX
   POP ECX
   RET
```
