Finally, the TEXTFILE.ASM program follows, in its entirety. Make sure you can read all of it—there’s nothing I haven't covered somewhere in the book. And if you want a challenge, here’s one for your next project: Expand TEXTFILE to read a text file, and write it out again with line numbers in front of each line of text. This sort of utility is called a text filter, and it’s one of the most common sorts of Unix programs.

```asm
; Source name      : TEXTFILE.ASM
; Executable name  : TEXTFILE
; Version           : 1.0
; Created date      : 11/21/1999
; Last update       : 12/4/1999
; Author            : Jeff Duttermann
; Description       : A text file I/O for Linux, using NASM 0.98

; Build using these commands:
; nasm -f elf textfile.asm
; nasm -f elf linlib.asm
; gcc textfile.o linlib.o -o textfile
;
; Note that this program requires several subroutines in an external
; library named LINLIB.ASM.
```

[SECTION] .text Section containing code

```asm
; These externals are all from the standard C library:
extern ebb
extern fclose
extern fgets
extern fprintf
extern printf
extern sscanf
extern time
```

```asm
; These externals are from the associated library LINLIB.ASM:
extern seedit      ; Seeds the random number generator
extern pull6       ; Generates a 6-bit random number from 0-63
extern newline     ; Outputs a specified number of newline chars
```

global main      Required so linker can find entry point

```asm
main:

    push ebb           ; Set up stack frame for debugger
    mov ebp,esp
    push ebx           ; Program must preserve ebp, ebx, esi, & edi
    push esi
    push edi

    ;; Everything before this is boilerplate; use it for all ordinary apps!
```

# 520 ASSEMBLY LANGUAGE STEP-BY-STEP

```asm
call seedit             ; Seed the random number generator
```

; First test is to see if command line arguments are at all.
;; If there are none, we show the help info as several lines.
;; forget that the first arg is always the program name, so there's
;; always at least 1 command-line argument!

```asm
mov eax, [ebp+8]      ; Load argument count from stack into eax
cmp eax, 1               ; If count is 1, there are no args
ja chkharg2            ; Continue if arg count is > 1
mov ebx, diskhelm ;; Put address of help file name in ebx
call diskhelp          ; If only 1 arg, show help info...
jmp gohome             ; and exit the program
```

; Next check for a command line argument 1
charg2:

```asm
mov ebx, [ebp+12]     ; Put pointer to argument table into ebx
push downlink      ; Push address of line count integer into scancf
push informat     ; Push address of integer formatting code
push draw [ebx+4]      ; Push pointer to arg(1)
call scancf            ; Call scancf to convert arg(1) to an integer
add esp,12             ; Clean up the stack
cmp eax, 1               ; Return value of 1 says we get a number
je chkdata             ; If we get a number, go on; else abort
mov eax, draw errl     ; Load eax with address of error message #1
call showerr           ; Show the error message
jmp gohome             ; Exit the program
```

; Here we're looking to see if there are more arguments. If there
;; are, we concatenate them into a single string no more than BUSIZE
;; chars in size. (Yes, I *know* what this strcat does...)
chkdata:

```asm
cmp draw [ebp+8],3   ; Is there a second argument?
je getjelines           ; If so, we have text to fill a file with
call randline          ; If not, generate a line of random text
                      ; Note that randline returns ptr to line in esi
jmp genfile            ; Go on to create the file
```

; we copy much command line as we have, up to BUSIZE
;; chars, into the line buffer. We skip the first two args
;; (at this point we know exist) but we know we have at least
;; one arg in arg(2). Going into this section, we know that
;; ebx contains the pointer to the arg table. All other bytes are off.

```asm
getlines: mov edx,2      ; We know we have at least arg(2), start there
mov edi,buffer        ; Destination pointer is start of char buffer
xor eax, eax           ; Clear eax to 0 for the character counter
cld                    ; Clear direction flag for up-memory movsb
```

```asm
grab: mov esi,[ebx+4] ; Copy pointer to next arg into esi
.copy: cmp byte [esi],0 ; Have we found the end of the arg?
```

# Coding for Linux 521

```asm
je .next               ; If so, bounce to the next
movsb                   ; Copy char from [esi] to [edi]; inc edi & esi
inc eax                ; Increment total character count
cmp eax,EBUFSIZE       ; See if we've filled the buffer to max count
je addnull             ; If so, add a null to & we're done
jmp .copy
```

```asm
.next: mov buff [edi],' '   ; Copy space to buff to separate args
inc edi                ; Increment destination pointer
inc eax                ; Add one to character count too
cmp eax,EBUFSIZE       ; See if we've filled buff
je addnull             ; If so, go down to add a null and we're done
inc edi                ; Otherwise, increment the argument count
cmp esp, dword [ebp+8] ; Compare against argument count
je addnull             ; If edi = arg count, we're done
jmp grab               ; And go back and copy it
```

```asm
addnull: mov buff [edi],0   ; Tuck a null on the end of buff
mov esi, dword          ; File code expects ptr to text in esi
```

;; We create a file to fill with the text we have:

```asm
genfile:
    push dword writecode   ; Push pointer to file/create code ('w')
    push dword filename    ; Push pointer to new file name
    call fopen             ; Create/open file
    add esp,8              ; Clean up the stack
    mov ebx,eax           ; Save handle of opened file in ebx

;; File is open. Let's fill it with text:
```asm
writeline:
    push ebx ; Push file handle on the stack
    push dword HELPLEN ; Limit length of text read
    push dwarf helpline ; Push address of help line buffer
    call fgets    ; Read a line of text from the file
    add esp,12             ; Clean up the stack
    cmp eax,0              ; A returned null indicates error or EOF
    je .donline           ; If we get 0 in eax, close up & return
    push dwarf helpline ; Push address of help line on the stack
    call printf   ; Call printf to display help line
    add esp,4              ; Clean up the stack
    jmp .rdln
```

```asm
.donline:
    push ebx              ; Push the handle of the file to be closed
    call fclose           ; Closes the while handle is on the stack
    add esp,4              ; Clean up the stack
    ret               ; Return control to the
```

;; Everything after this is boilerplate; use it for all ordinary apps!
gohome:
    pop edi               ; Restore saved registers
    pop esi
    pop ebx
    mov esp,ebp           ; Destroy stack before returning
    ret               ; Return to the C shutdown code

```
;; SUBROUTINES==================================================

```asm
----------------------------------------------------------------
; Disk-based mini-help      Last update 12/5/1999
; This routine reads text from a text file, the name of which is passed by
; way of a pointer to the name string in ebx. The routine opens the text file,
; reads the text from it, and displays it to standard output. If the
; be opened, a very short memory-based message is displayed.
```

```asm
diskhelp:
    push opcode ; Push pointer to open-for-read *
    push ebx      ; Pointer to name of help is passed in ebx
    call fopen    ; Attempt to open the file for reading
    add esp,8      ; Clean up the stack
    cmp eax,0      ; fopen returns null if attempted failed
    je .disk       ; Read help info from disk, else from memory
    call monhelp
    ret
.disk: mov eax,eax ; Save handle of opened file in ebx
.rdln:
    push ebx ; Push file handle on the stack
    push dword HELPLEN ; Limit length of text read
    push dwarf helpline ; Push address of help line buffer
    call fgets    ; Read a line of text from the file
    add esp,12             ; Clean up the stack
    cmp eax,0              ; A returned null indicates error or EOF
    je .donline           ; If we get 0 in eax, close up & return
    push dwarf helpline ; Push address of help line on the stack
    call printf   ; Call printf to display help line
    add esp,4              ; Clean up the stack
    jmp .rdln

.done:
    push ebx              ; Push the handle of the file to be closed
    call fclose           ; Closes the while handle is on the stack
    add esp,4              ; Clean up the stack
    ret               ; Go home
```

```asm
memhelp:
    mov eax,1
```
