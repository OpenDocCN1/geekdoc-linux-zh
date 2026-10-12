When you use any of these functions, include the header file dlfcn.h with this preprocessor directive:

```
#include <dlfcn.h>
```

Finally, here is a simple test program — dltest.c — that shows how to load and use the object defined in the shared library libobjj.so, which you create in the preceding section:

```
/* ----------------------------------------------*/
/* File: dltest.c 
 * Test dynamic linking.
 */
#include <dlfcn.h>  /* For the dynamic loading functions */
#include <stdio.h>

int main(void)
{
	void *dlobj;
	void *(*init_call)(char *name);
	void (*show_call)(void *data);
	void (*destroy_call)(void *data);

/* Open the shared library and set up the function pointers 
 */
if (dlobj = dlopen("libobjj.so.1",RTLD_LAZY))
{
	void *data;

	init_call=dlsym(dlobj,"init");
	show_call=dlsym(dlobj,"show");
	destroy_call=dlsym(dlobj,"destroy");

/* Call the object interfaces */
	data = (*init_call)("Test Object");
	(*show_call)(data);
	(*destroy_call)(data);
}

	return 0;
}
```

The program is straightforward: It loads the shared library, gets the pointers to the functions in the library, and calls the functions through the pointers.

You can compile and link this program in the usual way, but you must link with the -ldl option so you can use the functions declared in dlfcn.h. Here is how you build the program dltest:

```
gcc -o dltest dltest.c -ldl
```