# Tutorial

# Go functions

**Right** The multiple.go file uses the simple.go package, which is in another directory, with the help of the **GOPATH** variable.

**Across** The godoc utility can give you help about the use of the functions of a standard Go package.

![](bbox=[0.2, 0.15, 0.55, 0.4])

```
$ vi src/initFunction/initFunction.go
$ go build initFunction
$ go install initFunction
$ mkdir usr/usrInit
$ vi src/usrInit/useInit.go
$ go install usrInit
```

![](bbox=[0.57, 0.15, 0.95, 0.47])

Executing the previous code will generate the following output, where you can see that the init function is executed without any explicit call to it:

```
$ useInit
init function executed!
Hello!
```

However, the **init** function is not for printing silly messages; it is mainly used for performing serious initialisation tasks such as connecting to a database server.

# Using an external Go package

Sometimes packages are on the internet and you would prefer to use them by specifying their internet address. Imagine that there is a Go package named **simpleGitHub** stored somewhere at **GitHub.com** that contains a useful function. The exact location of **simpleGitHub** will be `https://github.com/mnactsouk/go/simpleGitHub`. You can use it in your own Go programs as follows:

```
import "github.com/mnactsouk/go/simpleGitHub"
```

After that, you will need to download the entire **simpleGitHub** package on your local machine, with the help of **go get**:

```
$ go get github.com/mnactsouk/go/simpleGitHub
```

The handy thing is that as soon as you execute the **go install** **githubExample.go** command, the **go** tool will automatically compile all required packages, which you can verify by looking at the contents of both **pkg** and **src** directories. When using **go get** to check out a new package, a new target directory is created inside **src**, named after the full import path.

You can find the full code as **githubExample.go** – you can see its source code in **Figure 3** (preceding page). **Figure 4** shows the contents of the **src** and **pkg** directories before and after executing **go install**.

Please note that the name of the package, which is **simpleGitHub**, is used in the code of **githubExample.go**, not its full path.

It is not compulsory to use every external package you download – you can just **go get** a Go program and examine its code without actually using it.

# Private variables and functions

This section will talk about how to define and use private variables and functions. What differentiates private variables and functions from public ones is that private ones can only be used internally. Controlling which functions and variables are public or not is also known as encapsulation.

# Advantages of packages

Packages make the design, implementation, and maintenance of large software systems much easier and simpler. Additionally, they allow multiple programmers to work on the same project without any overlapping.

A good package implemented for project-A can be reused in a different project without any additional work. The good thing with reusing an existing package is that the package has been already tested; as a result, an existing package contains fewer bugs and error than a newly developed one. Also, packages allow you to use the same function and variable names with other packages, because each package has its own scopes.

Put simply, the development and the use of packages can only bring advantages to your software system without introducing any risks. Therefore, if you are developing large software systems, you should definitely divide their functionality into packages that you can also reuse in other projects.