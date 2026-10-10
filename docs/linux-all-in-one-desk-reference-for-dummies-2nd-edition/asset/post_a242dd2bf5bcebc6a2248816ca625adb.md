
## Shared Libraries in Linux Applications

Most Linux programs use shared libraries. At a minimum, most C programs use the C shared library `libc.so.x`, where x is a version number. Using shared libraries is desirable because many executable programs can share the same shared library — you need only one copy of the shared library loaded into memory. Also, *dynamic linking* (wherein a program loads code modules and links with them at runtime) is becoming increasingly popular because it enables an application to load blocks of code only when needed, thus reducing the memory requirement of the application.

When a program uses one or more shared libraries, you need the program’s executable file, as well as all the shared libraries, to run the program. In other words, your program doesn’t run if all shared libraries are not available on a system.

> If you sell an application that uses shared libraries, make sure all necessary shared libraries are distributed with your software.

The subject of shared libraries is of interest to Linux programmers because use of shared libraries reduces the size of executables. In the following sections, I briefly describe how to create and use a shared library in a sample program.

## Examining the shared libraries that a program uses

Use the `ldd` utility to determine which shared libraries an executable program needs. Type the following `ldd` command to see the shared libraries used by a program (that was stored by GCC in the default file named `a.out`):

```
ldd a.out
```

Here is what `ldd` reports for a typical C program:

```
linux-gate.so.1 =>  (0x00000000)
libc.so.6 => /lib/1/libc.so.6 (0x4002a000)
/lib/ld-linux.so.2 (0x40000000)
```

A more complex program, such as The GIMP (an Adobe Photoshop-like program) uses many more shared libraries. To view its shared library needs, type the following command:

```
ldd /usr/bin/gimp
```

In this case you notice from the lengthy output that the program uses quite a few shared libraries, including the X11 library (`libX11.so.6`), The GIMP toolkit (`libgtk-x11-2.0.so`), the General Drawing Kit (GDK) library (`libgdk-x11-2.0.so.0`), the Math library (`libm.so.6`), and the C library (`libc.so.6`).

Almost any Linux application requires shared libraries to run.

## Creating a shared library

Creating a shared library for your own application is fairly simple. Suppose that you want to implement an object in the form of a shared library. (Think of an *object* as a bunch of code and data.) A set of functions in the shared library represents the object's interfaces. To use the object, you load its shared library and invoke its interface functions. (I show you how to load a library in the following section.)

Here is the C source code for this simple object, implemented as a shared library (you might also call it a *dynamically linked library*) — save this code in a file named `dynobj.c`:

```c
/*---------------------------------------------------*/
/* File: dynobj.c
 *
 * Demonstrate use of dynamic linking.
 * Pretend this is an object that can be created by
 * calling init and destroyed by calling destroy.
 */
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
/* Data structure for this object */
typedef struct OBJDATA
{
      char *name;
      int version;
} OBJDATA;
/*---------------------------------------------------*/
/* init
 * Initialize object (allocate storage).
 */
void* init(char *name)
{
      OBJDATA *data = (OBJDATA*)calloc(1, sizeof(OBJDATA));
      if(name)
        data->name = malloc(strlen(name)+1);
      strcpy(data->name, name);
      printf("Created: %s\n", name);
      return data;
}
/*---------------------------------------------------*/
/* show
 * Show the object.
 */
void show(void *data)
{
  OBJDATA *d = (OBJDATA*)data;
  printf("show: %s\n", d->name);
}
/* ------------------------------------------------------------------ */
/* destroy
 *
 * Destroy the object (free all storage).
 */
void destroy(void *data)
{
  OBJDATA *d = (OBJDATA*)data;
  if(d)
  {
    if(d->name)
    {
      printf("Destroying: %s\n", d->name);
      free(d->name);
    }
    free(d);
  }
}
```

The object offers three interface functions:

- `init` to allocate any necessary storage and initialize the object
- `show` to display the object (Here, it simply prints a message.)
- `destroy` to free any storage

To build the shared library named `libdobj.so`, follow these steps:

1. **Compile all source files with the -fPIC flag. In this case, compile the dynobj.c file by using this command:**
   ```
   gcc -fPIC -c dynobj.c
   ```
2. **Link the objects into a shared library with the -shared flag, and provide appropriate flags for the linker. To create the shared library named libdobj.so.1, use the following:**
   ```
   gcc -shared -Wl,-soname,libdobj.so.1.0 -o libdobj.so.1.0 dynobj.o
   ```
3. Set up a sequence of symbolic links so that programs using the shared library can refer to it with a standard name.

For the sample library, the standard name is `libdobj.so`, and the following commands set up the symbolic links:

```
ln -sf libdobj.so.1.0 libdobj.so.1
ln -sf libdobj.so.1 libdobj.so
```

4. When you test the shared library, define and export the `LD_LIBRARY_PATH` environment variable by using the following command:

```
export LD_LIBRARY_PATH=`pwd`:$LD_LIBRARY_PATH
```

After you test the shared library and you're satisfied that the library works, copy it to a standard location, such as `/usr/local/lib`, and run the `ldconfig` utility to update the link between `libdobj.so.1` and `libdobj.so.1.0`. These are the commands that you use to install your shared library for everyone's use. (You have to be `root` to perform these steps.)

```
cp libdobj.so.1.0 /usr/local/lib
/sbin/ldconfig
cd /usr/local/lib
ln -s libdobj.so.1 libdobj.so
```

## Dynamically loading a shared library

Loading a shared library in your program and using the functions within the shared library is simple. In this section, I demonstrate the way you do this action. The header file `<dlfcn.h>` (that's a standard header file in Linux) declares the functions for loading and using a shared library. Four functions are declared in the file `dlfcn.h` for dynamic loading:

- `void *dlopen(const char *filename, int flag);`: Loads the shared library specified by the filename and returns a handle for the library. The flag can be `RTLD_LAZY` (resolve undefined symbols as the library's code executes); or `RTLD_NOW` (resolve all undefined symbols before `dlopen` returns and fail if all symbols are not defined). If `dlopen` fails, it returns `NULL`.
- `const char *dlerror(void);`: If `dlopen` fails, call `dlerror` to get a string that contains a description of the error.
- `void *dlsym(void *handle, char *symbol);`: Returns the address of the specified symbol (function name) from the shared library identified by the handle (that was returned by `dlopen`).
- `int dlclose(void *handle);`: Unloads the shared library if no one else is using it.

When you use any of these functions, include the header file `dlfcn.h` with this preprocessor directive:

```c
#include <dlfcn.h>
```

Finally, here is a simple test program — `dltest.c` — that shows how to load and use the object defined in the shared library `libdobj.so`, which you create in the preceding section:

```c
/*-----------------------------------------------------------*/
/* File: dltest.c
 *
 * Test dynamic linking.
 *
 */
#include <dlfcn.h>  /* For the dynamic loading functions */
#include <stdio.h>

int main(void)
{
    void *dlobj;
    void *(*init_call)(char *name);
    void (*show_call)(void *data);
    void (*destroy_call)(void *data);

    /* Open the shared library and set up the function
       pointers */
    if (dlobj = dlopen("libdobj.so.1", RTLD_LAZY))
    {
        void *data;
        init_call = dlsym(dlobj, "init");
        show_call = dlsym(dlobj, "show");
        destroy_call = dlsym(dlobj, "destroy");

        /* Call the object interfaces */
        data = (*init_call)("Test Object");
        (*show_call)(data);
        (*destroy_call)(data);
    }
    return 0;
}
```

The program is straightforward: It loads the shared library, gets the pointers to the functions in the library, and calls the functions through the pointers.

You can compile and link this program in the usual way, but you must link with the -ldl option so that you can use the functions declared in `dlfcn.h`. Here is how you build the program `dltest`:

```bash
gcc -o dltest dltest.c -ldl
```
