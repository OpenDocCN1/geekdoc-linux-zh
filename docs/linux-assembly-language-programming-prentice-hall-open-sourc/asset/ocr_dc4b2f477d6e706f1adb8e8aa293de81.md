In the following sections, two examples of device drivers are presented. The purpose of these examples is to show what is involved in writing a device driver which incorporates some assembly code. The first driver is a toy. Its reason for existence is to serve as an example of a device driver. The second driver was written in response to a request from a friend who needed to input data from an external device as part of a research project involving the measurement of lizard metabolic rates. The goal of the research is a better understanding the mechanism by which environmental variations bring about lizard speciation (and also extinctions). So, although it is not a big program, it is not just a toy. The main feature the second driver has that the first one does not have is that it installs its own interrupt handler. The Morse Code driver merely adds some chores to those of an already installed handler.

# 11.3 Morse Code Speaker Driver

The basic structure which is used to connect device specific functions, such as `cq_write()`, with their generic counterparts, such as `write()` is the file operations structure.

# 11.3.1 The file_operations Structure

The definition of this structure is in `/usr/src/linux/include/linux/fs.h`. A simplified version of it is given here.

```
```
struct file_operations
{
	long long * lseek();
	int * read();
	int * write();
	int * readdir();
	int * poll();
	int * ioctl();
	int * mmap();
	int * open();
	int * flush();
	int * release();
	int * fsync();
	int * fasync();
	int * check_media_change();
	int * revalidate();
	int * lock();
};
```
```

All the components of this structure are pointers to functions. The function names are given exactly, but their parameter declarations are omitted and the return types are given using a familiar but nonportable x86 version, e.g. `int` instead of the more portable `ssize_t`. The use of types such as `ssize_t`, however valuable for the sake of getting the same code to compile and run on different architectures, has a serious downside when it comes to reading the code. For example to chase down the definition of `ssize_t`, we need to find

```
```
typedef __kernel_ssize_t ssize_t;
```
```

in `/usr/src/linux/include/linux/types.h` and then

```
```
typedef int __kernel_ssize_t;
```
```

in `/usr/src/linux/include/asm-i386/posix_types.h`. Learning an operating system should not turn into an exercise in using the `grep` command.

The creation of an instance of `struct file_operations` for a particular device is the key to writing a device driver. The biggest part of writing the driver is defining the functions in this structure. These functions handle the system calls which result in calls from the system to the device. Handling calls from the device to the system requires setting up an interrupt handler, or as in the case of the Morse Code speaker driver, piggy-backing off of an existing interrupt handler. Not all of the functions named in the `struct file_operations` structure are needed in every device. Unneeded components may simply be defined as