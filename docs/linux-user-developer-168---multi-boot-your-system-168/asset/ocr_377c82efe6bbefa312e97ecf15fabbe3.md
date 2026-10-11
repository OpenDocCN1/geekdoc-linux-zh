let's do something more interesting: let's find out how many binaries in the `/usr/bin` directory have the NX bit cleared. Thanks to the `execkstack` utility and its `-q` flag, you can query an ELF binary for the presence of the NX bit.

```
```
$ find /usr/bin -exec execkstack -q {} ";" 2>dev/
null|egrep --color=auto 	'X'
X 	/usr/bin/grub-mklayout
X 	/usr/bin/grub-mkrelpath
X 	/usr/bin/grub-mkimage
...
```

```

# ASLR and PIE

Address Space Layourt Randomization (ASLR) is a protection mechanism introduced in Linux and other operating systems that randomises the process memory space so that it is extremely difficult to find the address of functions or gadgets that an attacker could use in order to exploit a binary. Shared libraries are compiled with the `-fPIE` flag, allowing them to make use of the ASLR protection automatically. However, binary `.text` segments are not compiled with this protection unless they are built as Position Independent Executable (PIE). Grab your favourite text editor once again and write this code down:

```
```
#include <stdio.h>
void *getEIP () {
	return __builtin_return_address(0)-0x5;
}
int main(int argc, char** argv){
	printf("EIP located at: %p\n",getEIP());
	return 0;
}
```

```

Compile the code and then start to execute it a minimum of ten times (or more). You will get the same exact memory address for EIPB each time.

```
```
$ gcc -m32 aslr.c -o aslr
$ . ./aslrr
EIP located at: 0x80483f8
$ . ./aslrr
EIP located at: 0x80483f8
```

```

Now, let's give it another try but this time setting the PIE protection on the `.text` segment.

```
```
$ gcc -m32 -fPIE -pie aslr.c -o aslr
$ . ./aslrr
EIP located at: 0xff770d5c
$ . ./aslrr
EIP located at: 0xff77635c
```

```

Of course, if you do this with an ELF64 binary, the entropy will be greater and therefore the ASLR will become more reliable. There are plenty of papers exposing a way to bypass ASLR on 32 bit architectures using brute-force.

# Stack Canaries

One well-known method to inject alien code into an executable is by means of corrupting its stack. Open your favourite ASCII editor and write this code down:

```
```
#include <stdio.h>
#include <string.h>
void vuln(char *);
int main (int argc, char **argv){
	printf("Arg is: %s\n", *(argv+1));
	vuln(*(argv+1));
}

void vuln(char *arg){
	char buffer[10];
	strcpy(buffer, arg);
}
```

```

This is a classic buffer-overflow vulnerable code. Compile it the usual way and run it passing as many bytes as you need until you overflow the buffer:

```
```
$ gcc -m32 vuln.c -o vuln
$ ./vuln AAAAAAAAAAAAAAAAAAAAAAA
Arg is: AAAAAAAAAAAAAAAA
Segmentation fault
```

```

Now, execute it inside a `gdb` session until you get the `0x41414141` value for the EIP register. To achieve this, just increase the total number of "As" passed to the vulnerable program at each execution until you reach the desired value:

```
```
$ gdb ./vuln
(gdb) r AAAAAAAAAAAAAAAAAAAAAAA
Program received signal SIGSEGV, Segmentation fault.
0x41414141 in ?? ()
```

```

It is obvious that you can control the return address by corrupting the stack. If you want to overwrite the EIP register with, say, `0x54544432`, you can do it easily by altering the last 4 bytes passed as an argument like this:

```
```
(gdb) r "perl -e 'print \\x22 . \\x41""""
Program received signal SIGSEGV, Segmentation fault.
0x54544342 in ?? ()
```

```

The stack has been corrupted, that is undeniable. Now, compile the previous code with the stack guard protector to detect the corruption. The GNU C compiler offers this feature:

```
```
$ gcc -m32 -fstack-protector-all vuln.c -o vuln
```

```

![](bbox=[0.82, 0.14, 0.95, 0.4])

> "If you compile legacy code in a newer GNU/Linux distro, chances are that it will be built without protections"