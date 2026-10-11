rejects the connection in line 244 by closing the socket and looping back to step 6. In this program, the socket number is used as a sub-script into the `client[ ]` array, and, as such, it must be less than the value of `MAX_CLIENTS` in this program.

+   16. The usual `FILE` streams `rx` and `tx` are created and the buffering modes set in lines 251 to 271. Note, however, that in lines 263 and 264 the variable `mx` is increased to the new connected socket plus one, if the `mx` value needs increasing. Recall that `mx` must contain the maximum file descriptor value plus one, for the `select(2)` call.

+   17. The `client[ ]` entry for this client is further initialized by allocating a stack for the client and resetting its stack pointer `sp` to zero (lines 276 to 280).

+   18. Finally, `FD_SET` is used on `set rx_set` in line 282 to register the new client in the list of interesting file descriptors.

The steps just shown cover the server initialization and the accepting of new client connections. The following steps are used when clients send data to the server to be processed:

+   1. Line 226 invokes the `FD_ISSET` macro to test whether the socket `s` has any input data. If it has, the client accept process just described is executed in lines 227 to 283.

+   2. A `for` loop in line 288 iterates through all file descriptors less than the maximum value `mx`.

+   3. Line 289 causes processing to be skipped for socket `s`, since only `accept(2)` is used on that socket.

+   4. The `FD_ISSET` macro is called in line 291 to see if socket `c` has data waiting to be read (by testing descriptor set `wk_set`).

+   5. If step 4 evaluates as true, then the function `process_client( )` is called (line 292) with the socket number `c` as its input argument.

+   6. If the function call in step 5 returns the value `EOF` in line 292, then socket `c` is removed from the `rx_set` in line 293, using the `FD_CLR` macro. This is necessary because the socket has been closed by the `process_client( )` function and obviously will no longer return any data to be read.

+   7. The `for` loop in lines 301 to 304 perform the job of lowering the value of `mx` if it is possible. This is not essential, but it can help the performance of the `select(2)` call and the server when this value is maintained as small as possible.