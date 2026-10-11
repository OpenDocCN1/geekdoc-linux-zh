# Tutorial

# Compile new software

■ Protections and performance

Some of these protections can affect the program's throughput. For example, `relro`/`full relro` means that the `I-x` will resolve every library function's binary function to load immediately `reloc_1s` control. To more loading, some before-to-binary is responsive. Take this into account and always run performance tests.

Try to overflow the buffer now as you did before:

```
$ ./vuln `perl -e 'print "A"x18'`
*** stack smashing detected ***: ./vuln
terminated
```

# Full RELRO

Whenever running a new binary that makes use of shared libraries, the addresses of these libraries are resolved at execution time when a first call is made to any one of these libraries; this is called Lazy Binding. Because some addresses have to be figured out later on in the life of a binary loaded in memory, some ELF segments must be writable. This can lead to a well-known attack that overwrites the Global Offset Table (GOT) so that instead of making a call to, say, `printf`, once the attacker has been able to overwrite the address for `printf`, the program will end up calling some malicious injected code.

```
#include <stdio.h>
int main(int argc, char **argv){
    printf("Hello there!\n");
    return 0;
}
```

Save it and compile it this way:

```
$ gcc -m32 -no-builtin-printf relro.c -o relro
```

Disassemble the binary by running the `objdump` utility:

```
$ objdump -d relro > relro.S
```

Open the resulting disassembled file and look for the main function. Instead of calling `printf`'s address directly, there is a call to a symbol named `printf@plt`:

```
00048348 <main>:
...
80483f5: e8 06 ff ff ff    call
8048306 <HYPERLINK "mailto:printf@plt" printf@plt>
80483fa: 68 00 00 00 00    mov $0x0, %eax
```

Go to that offset, ie. `0048300`. You can clearly see that there is a jump into the GOT. The push `$0x0` is going to set the actual address for `printf` in the first GOT entry available for shared symbols, ie. `GOT[3]`:

![](bbox=[0.07, 0.74, 0.55, 0.94])

```
00048300 <printf@plt>:
8048300: ff 25 98 94 04 08  jmp
*<0x0894958>
8048306: 68 00 00 00 00    push $0x0
804830b: e9 e0 ff ff ff    jmp
80482f0 <.init+0x34>
```

Run the executable inside a `gdb` session to analyze the GOT. Because the `_got.plt` table is a section inside this ELF binary, you can ask `gdb` for its exact address:

```
$ gdb ./relro
(gdb) info sections _got.plt
0x089495c >0x0894964  0x0000068 _got.plt
ALLOC LOAD DATA HAS CONTENTS
```

Set a breakpoint right after the call to the `printf@plt` function and run the program:

```
(gdb) b *0x00483fa
Breakpoint 1 at 0x00483fa
(gdb) r
Hello there!
Breakpoint 1, 0x00483fa in main ()
```

Let's find out where the `printf` function is located:

```
(gdb) printf printf
$3 = <text variable, no debug info> 0x7f7e82c80
<"printf">
```

So `GOT[3]` must have the address `0x7f7e82c80`, which is the address for `printf`. To make sure this is so, dump the first 4 bytes for the `_got.plt` table:

```
(gdb) x/4 0x089495c
0x089495c <_GLOBAL_OFFSET_TABLE_> 0x0894958
0x7fff0598
0x7fff3598     0x7feac80
```

Because this is a writable address in the ELF binary, you can put whatever address you want in `GOT[3]`. You can find out which address equals to `GOT[3]` by doing pointer arithmetic:

```
(gdb) x/4 0x089495c+12
(0x0894968 <printf@.plt>          0x7feac80
```

So `GOT[3]` is located at `0x0894968`! Let's toy with the GOT, your goal will be to execute the system function instead of the "Hello world!" message. To do this, first find out where the address of `system` is:

```
(gdb) x system
$8 = <text variable, no debug info> 0x7f74c90
<"system">
```

Set a breakpoint before calling the `printf@plt` symbol:

```
(gdb) b *0x00483f5
Breakpoint 2 at 0x00483f5
```