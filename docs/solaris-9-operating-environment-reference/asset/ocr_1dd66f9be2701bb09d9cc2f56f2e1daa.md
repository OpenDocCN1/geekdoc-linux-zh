# 1184

# rpcgen

Note: This option is supported for backward compatibility only. You should always use it in conjunction with the -b option, which generates backward-compatible code. By default (that is, when you do not specify -b), rpcgen generates servers that can be invoked through port

+   -K seconds Change the default 120-second time that servers created by rpcgen and invoked through port monitors wait after servicing a request before exiting. To create a server that exits immediately on servicing a request, use -K 0. To create a server that never exits, use -K -1.

+   - When monitoring for a server, some port monitors, like listen(1M), always spawns a new process in response to a request. If you know that a server is used with a monitor, the server should exit immediately on completion. For servers, rpcgen with -K 0.

+   -1 Compile into client-side stubs.

+   -L When the servers are started in foreground, use syslog(3) to log the server errors instead of printing them on the standard error.

+   -m Compile into server-side stubs, but do not generate a main routine. This option is useful for doing callback routines and for users who need to write their own main routine to do initialization.

+   -N Generate multithread-safe stubs for passing arguments and results between rpcgen-generated code and user-written code. This option is useful if you want to use threads in your code.

+   - Enable procedures to have multiple arguments. This option uses a style of parameter passing that closely resembles C. So, when passing an argument to a remote procedure, you do not have to pass a pointer to the argument but can pass the argument itself. This behavior is different from the old style of rpcgen-generated code. To maintain backward compatibility, this option is not the default.

+   -n netid Compile into server-side stubs for the transport specified by netid The netconfig database should contain an entry for netid You can specify this option more than once to compile a server that serves multiple transports.

+   -o outfile Specify the name of the output file. If one specified, use standard output (-c, -h, -m, -n, -s, -Sc, -Sm, and -t modes only)

+   -s nettype Compile into server-side stubs for all transports belonging to the class nettype The supported classes are netpath, visible, circuit_v, datagram_n, datagram_v, tcp, and udp (rpc(3N) for the meanings associated with these classes). You can specify this option more than once. Note that the transports are chosen at runtime and not at compile.

+   -Sc Generate a sample client code that uses remote procedure calls.

+   -Sm Generate a sample Makefile that can be used for compiling the application.

+   -Ss Generate a sample server code that uses remote procedure calls.