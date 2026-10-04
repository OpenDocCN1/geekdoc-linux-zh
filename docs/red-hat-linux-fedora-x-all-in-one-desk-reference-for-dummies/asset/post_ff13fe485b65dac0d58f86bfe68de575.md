
# Understanding Perl Packages and Modules 803

## Using a module

You can call the `require` function or use the `use` function to include a Perl module in your program. For example, a Perl module named `Cwd` (defined, as expected, the `Cwd.pm` file) provides a `getcwd` subroutine that returns the current directory. You can call the `require` function to include the `Cwd` module and call `getcwd` as follows:

```
require Cwd; # You do not need the full file name
$curdir = Cwd::getcwd();
print "current directory";
```

The first line loads the `Cwd.pm` file into this program — you do not have to specify the filename; the `require` function automatically adds `.pm` to the module's name to figure out which file to include. The second line shows how you call a subroutine from the `Cwd` module. When you use `use` to include a module, you must invoke each subroutine with the `Module::subroutine` syntax.

If you rewrite this example with the `use` function in place of `require`, it takes the following format:

```
use Cwd;
$curdir = getcwd(); // no need for Cwd:: prefix
print "current directory: $curdir\n";
```

The most significant difference is that you no longer need to qualify a subroutine with the module name prefix (such as `Cwd::`).

You can call either `require` or use `use` to include a module in your program. Remember the following nuances when you use these functions:

- When you include a module by calling `require`, the module is included only when the `require` function is invoked as the program runs. You must use the `Module::subroutine` syntax to invoke any subroutines from a module you include with the `require` function.

- When you include a module by calling `use`, the module is included in the program as soon as the `use` statement is processed. Then, you can invoke subroutines and variables from the module as they are part of your program. You do not need to qualify subroutine and variable names with a `Module::` prefix.

You might want to stick to the `use Module:` syntax to include modules in your program because this syntax lets you use a simpler syntax when you call subroutines from the module.

![](img/d9230b719dc0efd80851f363d8c6f571_829_0.png)

# 804 Using Objects in Perl

## Using Objects in Perl

An object is a data structure together with the functions that operate on data. Each object is an instance of a class that defines the object's type. For example, a rectangle class may have the four corners of the rectangle as data; functions such as one that computes the rectangle's area; and another draws the rectangle. Then, each rectangle object can be an instance of the rectangle class, with different coordinates for each of the four corners. In this sense, an object is an instance of a class.

The functions (or subroutines) that implement the operations on an object's data are known as methods. That's terminology borrowed from Smalltalk, one of the earliest object-oriented programming languages.

Classes also suggest the notion of inheritance. You can define a new class of objects by extending the data or methods (or both) of an existing class. Common use of inheritance is to express the IS relationship among various classes of objects. Consider, for example, geometric shapes. Because a circle IS A Shape and a rectangle IS A Shape, you can say that the circle and rectangle inherit from the shape class. In this case, the shape class is called parent class or base class.

![](img/d9230b719dc0efd80851f363d8c6f571_830_0.png)

The basic idea behind object-oriented programming is that you can package the data and the associated methods (subroutines) of an object so they work like a black box — input generates output, without your having to specify every detail of how to get the job done. Programmers access the object without knowing the inner workings of the methods. Typically, a programmer create an object, invoke methods to get or set attributes (that another name for the object's data), and destroy the object. In this section, I show you how to use objects in Perl. With this knowledge in hand, you can exploit objects as building blocks for

# Understanding Perl Objects

Perl implements objects using modules, which package data and subroutines in a file. Perl presents the following simple model of objects:

- A class is a Perl module that provides the methods to work with the object.

- A method is a Perl subroutine that expects the object reference as the first argument.

# Understanding Perl Objects 805

Object implementers follow certain rules and provide certain methods in a module that represents a class. However, you really don't need to know much about an object's implementation to use it in your Perl program. For practical purposes, all you need to know the steps you have to follow when you use an object.

Book IX
Chapter 4
Programming in Perl

## Creating and accessing Perl objects

An especially useful object is the Shell object, which is implemented by the Perl module Shell.pm. That module comes with the Perl distribution and is in `/usr/lib/perl/5.8.3` (for Perl Version 5.8.3).

As the name implies, the Shell object is meant for running shell commands from within Perl scripts. You can create a Shell object and run shell commands from within Perl scripts. To use the Shell, follow these general steps:

- 1. Include the following line in your program:
  use Shell;

- 2. Create a Shell object:
  my $sh = Shell->new();

- 3. Use the Shell object to run commands:
  $result = $sh->run("ls -l");

- 4. Capture the output of the command:
  my @output = $sh->output();

- 5. Process the output using a for loop:
  ```
  foreach my $line (@output) {
    print "$line\n";
  }
  ```

# 806 Using Perl Objects

## Using English

Perl includes several special variables with strange names, such as $_ (for the default argument) and $ (for error messages). When you read a program, guessing what special variable can be difficult. As a helpful gesture, Perl provides the English module (English.pm), which enables you to use understandable names. To use the English module, include the following line in your program:

```
use English;
```

After that, you can refer to $_ as $ARG and $ as $ERRNO. (These "English" names can still be a bit cryptic, but they're definitely better than the originals).

The English module is handy because it lets you write Perl scripts by meaningful names. To find out more about Perl special variables and their English names, type man pervar in a terminal window, or better yet, point your Web browser to www.perdoc.com/perl5.8.0/pod/pervar.html

# Appendix: About the DVD

**In This Appendix**

- System requirements
- DVD installation instructions
- What you can find on the DVD
- Troubleshooting

Make sure that your computer meets the minimum system requirements in the following list. If your computer doesn't match up most of these requirements, you may have problems using the software and files on the DVD.

- A PC with processor running at400 MHz or faster for graphical installation
- At least 192MB of RAM installed on your computer for graphical installation (256MB recommended)
- At least 520MB free space on your hard disk for a minimal installation; 5GB of free space recommended if you plan to install most packages so you can try out everything covered in this book
- A DVD-ROM drive (if you have only a CD-ROM drive, use the included coupon to order Fedora Core on CD-ROMs or download and burn your CDs — see Book I, Chapter 5 for instructions)
- A graphics card and monitor capable of displaying at least 256 colors
- A sound card
- Ethernet network interface card (NIC) or modem with a speed of at least 56 Kbps

# DVD Installation Instructions

Installing Fedora Core from the DVD is easy as long as you can boot your PC from the DVD-ROM drive.
