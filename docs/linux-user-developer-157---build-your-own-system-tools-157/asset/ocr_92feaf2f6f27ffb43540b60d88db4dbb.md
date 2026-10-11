# Go

```
```
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
```

# Rust

```
```
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
```

# Python

```
```
#!/usr/bin/python
import sys
import shutil

if len(sys.argv) == 3:
    input = sys.argv[1]
    output = sys.argv[2]
    shutil.copy2(input, output)
```
```

# Perl

```
```
#!/usr/bin/perl -w
use strict;
use File::Copy;

my $input = shift;
my $output = shift;

copy($input, $output) ||
die "File copying failed: $!";

exit 0;
```
```

# Go

Go is an open source programming language that makes it easy to build reliable and efficient software.

The code to the left shows the Go version of the cp utility, which uses a fairly unconventional approach as it reads the whole file and then copies it all at once — this method might not be so efficient for really large files.

Apart from necessary error checking, the cp() function does the job using two Go functions without the programmer having to deal with any other issues. You can generate an executable file by running **go build copy.go**.

# Rust

Rust is a new systems programming language that tries to avoid unpleasant bugs caused by unsafe code. The compiler is clever enough to produce warnings and errors with useful messages that assist you in avoiding bugs and correcting errors.

The next piece of code shows the Rust version of our utility. The good thing is that it also copies the permission bits of the original file to the destination file. However, Rust code looks unpleasant and it’s hard to read; the code is more beautiful.

At the time of writing, the current version of Rust is 1.2. Nonetheless, Rust is under development, which means your program might need changing when a new version comes.

# Python

Python can also be used for systems programming; it might not be the best option to write a highly available production web server, but it can be used for testing and prototyping with great success. You can also write useful command line utilities without the need to write too much code, as you can see from the code showing the Python version of the cp utility.

# Perl

Perl is a well-known programming language that can do almost anything including systems programming. It might not be the best language to write a production DNS server that accepts thousands of requests, but it is a very capable programming language for developing useful command-line utilities.

The code at the bottom of the page shows the Perl version of the cp utility. It is small, comprehensive and easy to read.

![](bbox=[0.35, 0.38, 0.6, 0.6])

![](bbox=[0.15, 0.05, 0.85, 0.14])