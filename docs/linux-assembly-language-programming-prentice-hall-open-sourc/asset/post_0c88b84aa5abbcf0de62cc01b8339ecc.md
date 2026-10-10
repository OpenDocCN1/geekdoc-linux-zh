
| [EAX] | DS | [AX] | illegal! |
|---|---|---|---|
| [EBX] | DS | [BX] | DS |
| [ECX] | DS | [CX] | illegal! |
| [EDX] | DS | [DX] | illegal! |
| [ESI] | DS | [SI] | DS |
| [EDI] | DS[1] | [DI] | DS[1] |
| [ESP] | SS | [SP] | SS |
| [EBP] | SS | [BP] | SS |

[1] ES with string instructions

The default segment for both immediate addresses and for addresses stored in the BX register is the DS segment.

Default segments exist in 32-bit code as well. In fact, that is what makes it possible to do programming without reference to segments, as is done in chapter 8. The Linux programs there all make use of a default segment. It is actually a 4 Gig segment. Setting up big segments like this is discussed in chapter 13. In x86 Linux, the CS, DS, ES, and SS segments all refer to the same 4 Gig segment. So the programmer has no options, and the default segment is always okay.

## 12.2 Edlinas Environment Variables

Many assemblers have directives which allow variables to be defined and then used in subsequent expressions. In NASM, the syntax for such a directive is

```
var equ value
```

In Edlinas, it is

```
var . = value
```

In Edlinas, there are built-in variables whose values control the behavior of the assembler and the simulator. One of these is USE, which determines whether the assembler uses 16-bit or 32-bit coding. The default is 32. DOS programs require 16.

NASM uses a directive called *BITS*. For example, to specify 16-bit code in NASM, the line

```
BITS 16
```

does the trick. Another environment variable is *DOTO*. It determines the format of .o files saved by Edlinas. The default is *ELF*. DOS needs the *COM* format.

NASM governs the format of the output file using a command line switch. To get a *COM* format in NASM, the `-f bin` switch works. It is also the default so that no switch at all will do the same thing. A file with this format has essentially no extra code at all. It is just a plain binary file.

Edlinas environment variables may also be defined in an *EDL.INI* file or from the > prompt.

## 12.3 Fixed Memory Areas

Real mode allows the programmer to use physical memory addresses. Memory addresses specified in real mode are used on the address bus, just like I/O addresses. This gives the programmer unimpeded access to memory. In this section, as an exercise in the use of real mode addresses, we consider two areas of memory which are defined by fixed physical addresses: the video buffer and the keyboard buffer. The location of the video buffer is fixed in the hardware. But the keyboard buffer is only fixed by DOS, and hence it can be moved. Referring to Figure 12-1, programs which access these physical memory areas directly are definitely "rude" programs as opposed to "polite" programs.

# Figure 12-1. Unprotected Operating System such as DOS

![](img/a3d6758e6e21b80b35e1b981ecbc1234_167_0.png)

### 12.3.1 Video Buffer

On standard PCs, there is a region of memory starting at the address B8000H called the *video buffer*. In the most commonly used video text mode, the video buffer holds the text information which is displayed on the screen. A very simple, but somewhat tedious, way to output information on a PC is to store ASCII codes in this buffer. (See Table 11.1.)

The address B8000H is the actually address of the ASCII code for the character in the upper left-hand corner of the screen. See Figure 12-3. The next byte, which is at B8001H, contains the *attribute* information for this same character. Table 12.2 shows how the eight bits of an attribute byte are used. B8002H is the ASCII code of the second character in the first row; B8003H is its attribute byte, and so on. The top row consists of 80 characters, or 160 bytes, since each character takes two bytes of storage. One screenful is 25 rows × 80 columns × 2 bytes per character = 4000 bytes. The buffer actually contains 4096 bytes = 1000H.

# Figure 12-3. Upper Left at B8000 through Lower Right at B8F9E

![](img/a3d6758e6e21b80b35e1b981ecbc1234_167_1.png)

Program 12.1 prints "Hello" on the screen by storing five ASCII codes into the video buffer. Figuring the address of the thirty-seventh character on line 13 in hex,

```
B8000H + DxA0 + 24H x 2 = B8000H + 820H + 48H = B8868H
```

Program 12.2 is a little 17-byte program which colors the screen yellow on blue by writing to all the attribute bytes in the video buffer. It begins at FFFH and counts down by twos.

### 12.3.2 Keyboard Buffer

When a key is either pressed or released, an interrupt is generated. On an ISA machine this interrupt is allotted, IRQ #1, which in turn is reported by the interrupt controller as interrupt number 9. (See Table 9.3.)

The DOS interrupt service routine 9 interrogates the keyboard at I/O port 64H and deposits characters it receives from there in a tiny buffer located at 41EH. The characters come in from the keyboard as *scan codes*. The ISR converts each scan code to an ASCII character and stores both a scan code and an ASCII code in the buffer. From this buffer, the keys are picked up by the application program or the command line interpreter. The two bytes stored at 41A point to the next departing bytes. In Figure 12-4, there is one key waiting to be picked up. It is the letter C, whose ASCII code is 43H. 2E is its scan code. The two bytes stored at 41C point to the location where the next arriving bytes will be stored. Since the departing pointer is only two bytes behind the arrival pointer, this means there is only one character in the buffer, C in this case. Both pointers wrap around when they reach 43E. For this reason, the buffer is called a *circular buffer*.

**Program 12.1**

```
USE    . = 16
DOTO   . = COM

; Write Hello by storing ASCII codes into the video buffer.

        MOV AX, 0B886H ; First 4 digits of B8868H
        MOV DS, AX
        MOV DI, 8      ; Last digit of B8868H
        MOV AH, 72     ; ASCII for H
        MOV [DI], AH   ; Store the character.
        ADD DI,2       ; Next odd address
        MOV AH, 101    ; ASCII for e
        MOV [DI], AH   ; Store the character.
        ADD DI,2
        MOV AH, 108    ; ASCII for l
        MOV [DI], AH   ; Store the character.
        ADD DI,2
        MOV AH, 108    ; ASCII for l
        MOV [DI], AH   ; Store the character.
        ADD DI,2
        MOV AH, 111    ; ASCII for o
        MOV [DI], AH   ; Store the character.
        RET            ; Return to DOS
```

Figure 12-4. DOS Keyboard Buffer

| | | | | | |
|---|---|---|---|---|---|
| Keyboard Buffer (ASCII - Scan) | | | | | |
| 41E | 41F | 420 | 421 | 422 | 423 |
| 31 | 02 | 43 | 2E | 4C | 26 |
| ↑ | | ↑ | | | |

Head pointer: 20
Tail pointer: 22

Program 12.3 stores the string DIR into the keyboard buffer.

## 12.4 Real Mode Interrupts

When "polite" user programs want access to peripherals, they call the operating system. In a protected operating system, there is no choice about this. In an unprotected operating system like DOS, the call to the operating system is optional. (See Figure 12-1.) Just as the programs in section 12.3 accessed peripherals by barging in on their private memory space, "rude" programs can also access peripherals by using IN and OUT instructions.

Like Linux, the DOS operating system is accessed using software interrupts. The interrupt most used for access to DOS is INT 21H. To call one of the functions available under INT 21H, its number is stored in the AH register before the interrupt is called.

### 12.4.1 DOS Interrupts

To call the DOS function which outputs a character to the cursor location on the screen, the function number 2 is stored in the AH register and the ASCII code of the character to be printed is stored in the DL register. (Table 11.1 shows the ASCII code.) For example, the following code would print the letter H.

**Program 12.2**

```
USE   . = 16
DOTO  . = COM

      MOV AX, 0B800H ; Video buffer begins at B8000H
      MOV DS, AX
      MOV BX, 0FFFH  ; Odd address ending the 4K buffer.
      MOV AH, 1EH    ; Yellow on blue.
AGN:  MOV [BX], AH   ; Attribute goes into odd address
      DEC BX         ; Get next
      DEC BX         ; odd address
      JNS AGN        ; Continue till the beginning of the buffer
      RET            ; Return to DOS
```

| Bit | Usage               | Example |
|-----|---------------------|---------|
| 7   | Blinking            | 0       |
| 6   | Background Red      | 0       |
| 5   | Background Green    | 0       |
| 4   | Background Blue     | 1       |
| 3   | Foreground Intensity| 1       |
| 2   | Foreground Red      | 1       |
| 1   | Foreground Green    | 1       |
| 0   | Foreground Blue     | 0       |

**Program 12.3**

```
      MOV AH, 2
      MOV DL, 72 ; ASCII code for H.
      INT 21H

USE   . = 16
DOTO  . = COM

      MOV AX, 40H  ; Make 400H the base address
      MOV DS, AX   ; of the DS segment.
```
