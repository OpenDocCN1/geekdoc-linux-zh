
## GO BEYOND C

There are many other programming languages for you to work with, although none are as mature as C. There exist many programming languages that can help you perform system tasks. All programming languages implement their own functions by using C system calls because it is the only interface for talking to the Linux kernel.

The example program that is going to be implemented on all six programming languages is a minimalistic version of the cp command line utility. The presented implementations in C++, Rust, Go, Perl and Python are not the only ones enabled or offered by each programming language. They are presented here in order to give you a quick sense of each programming language.

### C and C++

When it comes to systems programming, C++ can be almost identical to C. Their only difference is that in C++ you can organise your code differently because C++ is an object-oriented programming language.

Just to the right, you can see both the C and C++ versions of the cp utility. The C++ version uses an unorthodox approach and performs no error checking, whereas the C code is, more or less, the standard way of writing the cp utility. There exist other techniques that can be used for file copying, but the general idea will be the same. The biggest advantage of the C approach is that if an error occurs during the execution of the program, you will know exactly which system call caused the error. Think about it a little: you will know the precise line of the C code and the exact reason behind the problem! You cannot tell the same from the C++ version of the program because it uses higher-level commands that do many things using just one command.

It’s not strange that the C code of the cp command is the longest of all presented code as the functions are primitive.

### Best language?

You may ask which is the best programming language for Linux systems programming. The easy answer is C, because Linux is written in C and C is more mature as a programming language than the alternatives.

The main advantage of programming languages such as Perl and Python is the fact that they can easily interact with other things like databases. Additionally, they can implement a lot of functionality using just a few lines of code. However, they hide too many low-level details from programmers and make the potential to become the next big thing in systems programming. Another interesting language that you might want to check, as soon as the necessary tools become available on Linux, is Swift from Apple.

```c
#include <fcntl.h>
#include <unistd.h>
#include <stdio.h>

int myCP(char *file1, char *file2)
{
  FILE *rRead, *fWrite;
  rRead = fopen(file1, "r");
  fWrite = fopen(file2, "w");

  if (rRead == NULL) {
    printf("Could not open %s\n", file1);
    return -1;
  }

  if (fWrite == NULL) {
    printf("Could not create %s\n", file2);
    return -1;
  }

  size_t len;
  unsigned char buffer[8192];
  while ( (len = fread(buffer, 1, sizeof buffer, rRead)) > 0 ) {
    size_t written = fwrite(buffer, 1, len, fWrite);
    if (written != len)
      printf("There was an error: %zu <> %zu\n", written, len);
  }
  fclose(rRead);
  fclose(fWrite);
  return 0;
}

int main(int argc, char *argv[])
{
  if (argc != 3) {
    printf("Please provide the correct number of arguments!\n");
    exit(-1);
  }
  return myCP(argv[1], argv[2]);
}
```

```cpp
#include <iostream>
#include <fstream>

int main(int argc, char *argv[])
{
  std::ifstream src(argv[1], std::ios::binary);
  std::ofstream dst(argv[2], std::ios::binary);

  dst << src.rdbuf();
}
```

### Kernel development

Since the Linux kernel is written in C, you might wonder how much of this applies to kernel development. The good news is that system call handling and other techniques discussed here will be reusable, although there are key differences – a main() function isn’t required in kernel modules, for example, because kernel programming is asynchronous. It’s worth dipping into the Foundation’s guide. bit.ly/IK7uHC.

![](img/e7f197876caa0b235fb5da2d16a578ea_25_0.png)

## Go

```go
package main
import (
	"fmt"
	"os"
	"io/ioutil"
)

func cp(source, destination string) {
	data, err := ioutil.ReadFile(source)
	if err != nil {
		fmt.Println("Error reading the file!")
	}
	err = ioutil.WriteFile(destination, data, 0644)
	if err != nil {
		fmt.Println("Error copying the file")
	}
}

func main() {
	if len(os.Args) != 3 {
		fmt.Println("You should use exactly")
		fmt.Println("two command line arguments!")
		os.Exit(-1)
	}
	cp(os.Args[1], os.Args[2])
}
```

## Rust

```rust
use std::env;
use std::fs;

fn main() {
    let args: Vec<_> = env::args().collect();
    if args.len() != 3
    {
        let input = ::std::env::args().nth(1).unwrap();
        println!("Input: {}", input);
        let output = ::std::env::args().nth(2).unwrap();
        println!("Output: {}", output);
        fs::copy(input, output);
    }
}
```

## Python

```python
#!/usr/bin/python
import sys
import shutil

if len(sys.argv) == 3:
    input = sys.argv[1]
    output = sys.argv[2]
    shutil.copy2(input, output)
```

## Perl

```perl
#!/usr/bin/perl -w
use strict;
use File::Copy;

my $input = shift;
my $output = shift;

copy($input, $output) ||
die "File copying failed: $!";

exit 0;
```

### Go

Go is an open source programming language that makes it easy to build reliable and efficient software.

The code to the left shows the Go version of the cp utility, which uses a fairly unconventional approach as it reads the whole file and then copies it all at once — this method might not be so efficient for really large files.

Apart from necessary error checking, the cp() function does the job using two Go functions without the programmer having to deal with any other issues. You can generate an executable file by running `go build copy.go`.

### Rust

Rust is a new systems programming language that tries to avoid unpleasant bugs caused by unsafe code. The compiler is clever enough to produce warnings and errors with useful messages that assist you in avoiding bugs and correcting errors.

The next piece of code shows the Rust version of our utility. The good thing is that it also copies the permission bits of the original file to the destination file. However, Rust code looks unpleasant and it’s hard to read; the code is more beautiful.

At the time of writing, the current version of Rust is 1.2. Nonetheless, Rust is under development, which means your program might need changing when a new version comes.

### Python

Python can also be used for systems programming; it might not be the best option to write a highly available production web server, but it can be used for testing and prototyping with great success. You can also write useful command line utilities without the need to write too much code, as you can see from the code showing the Python version of the cp utility.

### Perl

Perl is a well-known programming language that can do almost anything including systems programming. It might not be the best language to write a production DNS server that accepts thousands of requests, but it is a very capable programming language for developing useful command-line utilities.

The code at the bottom of the page shows the Perl version of the cp utility. It is small, comprehensive and easy to read.

![](img/e7f197876caa0b235fb5da2d16a578ea_26_0.png)

![](img/e7f197876caa0b235fb5da2d16a578ea_26_1.png)

## RUNNING WINDOWS APPS WITH WINE

Wine gets stubborn Windows-only apps running comfortably on Linux – so no more need to dual boot!

As your day-to-day computer use – from games, through office and collaboration apps, to social media – moves to the web browser, relying on cross-platform, free and open source technologies, there’s a fairly level playing field between Linux and its proprietary rivals, most particularly Microsoft Windows. Before free software advocates rejoice too much, there remains one road block for many users looking to transition away from the spyware-ridden recent versions of Windows: a stubborn collection of legacy or proprietary software available only for Microsoft’s platform.

Whether you’re an office user tied to macros written for MS Office, a worker dependant upon custom proprietary software for their day-to-day work, or a gamer who simply must have their fix, a serious move to Linux will only happen if you can happily run your critical software on your new favourite OS. Enter Wine.

WINE stands for WINdows Emulator – or for Wine Is Not an Emulator; the ‘not’ version making it clear that Wine emulates no processor code, but instead replaces system calls to libraries and the Windows kernel with its own processes. The Wine team have done a fine job of keeping up with all of Windows’ changes and developments, with the winetricks program handling workarounds and tweaks for programs that won’t run on default settings.

In this, we are complemented by PlayOnLinux, which makes installing Windows programs on versions of Wine easier, keeping them partitioned in different containers.
