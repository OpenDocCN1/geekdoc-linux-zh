Compiling the executable of `useSimple.go` inside the `. / bin` directory requires the following step:

```
```
$ go install useSimple
$ ls -l -n bin/useSimple
-rw-r--xr-x 1 mtsouk mtsouk 1824408 Jun 3 00:38
bin/useSimple
```
```

Executing `useSimple` produces the next output:

```
```
$ useSimple
This is the main function of the main package!
This is the main function of the single
package!
This is the foo function!
Calling simple.Bar: 5
```
```

If for some reason you import a package but forgot to use it, the Go compiler will generate an error message and refuse to finish the compilation process:

```
```
$ go build useSimple
# useSimple
src\useSimple\useSimple.go:5: imported and not used: "simple"
```
```

Should you wish to ignore such a message, you can use the import statement as follows:

```
```
import _ "simple"
```
```

Using the `"_"` as the package identifier will make the compiler ignore the fact that the package is not being used – the only sensible reason for bypassing the compiler is when you have an `init` function in your unused package that you want to be executed. Keep reading to learn more about the purpose of the `init` function.

Please make sure that you fully understand Go environment variables and the build process before continuing with the rest of the tutorial.

# ## The init function

Every Go package can have a function named `init` that is automatically executed at the beginning of the execution time. The following code illustrates the use of the `init` function:

```
```
package initFunction

import "fmt"

func main() {
	fmt.Printf("init function executed!\n")
}

func Foo() {
	fmt.Printf("Foo function executed!\n")
}
```
```

The related Go code is saved as `initFunction.go`; therefore,

![](bbox=[0.44, 0.17, 0.92, 0.51])

# ## Various uses of the go tool

The `go` tool can do many more things related to package files. The `single` `move` object file to the `clean` command, which allows you to browse object files from a package’s source directories.

You will have to use the `-f` flag in order to specify which program or package you want to clean up. If you are not sure about the effects of the `go clean`, you can use it with the `-n` flag; this tells the program to remove commands it will execute, without actually executing them. Finally, the `-x` flag tells the program to print the commands it executes. The `go clean` command is particularly useful when you want to transfer your project to other machines.

```
```
$ go clean -n -x github.com/mtsouk/go/simpleGitHub
```
```

using it will require the following code, as found in `useInit.go`:

```
```
import (
	"fmt"
	"initFunction"
)

func main() {
	fmt.Printf("Hello\n")
}
```
```

Building and executing `useInit.go` requires the following steps:

```
```
$ mkdir src/initFunction
```
```