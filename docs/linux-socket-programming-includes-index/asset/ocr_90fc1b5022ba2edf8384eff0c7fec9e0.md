This does result in the problem of getting information back unless you let the return value be the result. You can get around passing everything by value, but at some point the program does have to send the data. With this approach, you still pass your parameters by reference, but the program does copy the data at least at the very last stage.

The following example shows a prototype of an interface of the getphoto() service call. The types image_t and host_t are custom types that you create. If you are adventurous, you can return the result by value as well. Still, you might want to leave the return value open to indicate an error; if you return a structure or type by value, you can't effectively detect errors.

```
```cpp
/*** Pass-by-value example - call a camera server to get ***/
/*** recent snapshot. ***/
image_t *getphoto(host_t host);
```
```

> Returning Vectors by Value
> 
> The C language permits you to return a vector by value. However, the implementation is compiler-specific and may surprise you. Because of the way some processors handle the hardware stack, the compiler may not actually copy the result to the stack. Instead, it may create a local or static variable and pass back the variable reference. Upon returning, the caller then copies the value into the appropriate destination. This may have a significant side effect in multithreaded programs. Alternatively, some compilers may even be "smart" and note the destination before calling the function. As the function populates the vector, it's really revising the actual destination.

The parameters themselves are a particular problem. Most programmers do not designate which parameters are input only, output only, or input/output. But, because the interface has to determine which parameters to send and which to fill, you need to indicate that in the interface somehow. Often the documentation is the interface. Consider the following example:

```
```cpp
/*** Network interface example ***/
/* ----------------- PUBLICATION NOTES ----------------- */
/* getuserinfo - get the finger information from a host */
/*    user - (input) user's login id           */
/*    host - (input) the external host name    */
/*    data - (output) the results of the call   */
/* RETURN VALUE: success or failure (check errno) */
int getuserinfo(char* user, char* host, userinfo_t *data);
```
```