Step 8 is the point where the server program calls the function `accept(2)`. This is where the server control "blocks." The server will not execute any further instructions unless a client connects. After a connection has taken place, the `accept(2)` call will return in line 122. Note that variable c holds the client socket that has been returned by the `accept(2)` function call.

Client request processing continues in steps 9 to 11. Then the server repeats step 8 to await the next client connection.

The following shows how to make and invoke the server program:

![](bbox=[0.07, 0.31, 0.92, 0.55])

The output shows the server being run in the background, without any command-line parameters. The `telnet` command connects to it to test it out. Notice that port `9099` is specified on the telnet command line.

The returned output from the server is purposely different from the standard daytime server. The standard daytime server abbreviates the weekday name. Because the session output shows the full weekday name, you can be confident that you contacted your server instead of the standard server.

Before proceeding to the next section, bring down your server. The server is designed to loop forever until you kill it. So you can simply list your jobs and kill it off as follows:

![](bbox=[0.07, 0.81, 0.92, 0.9])

The `jobs` command is the `bash` shell built-in that enables you to see which processes you started and left to run in the background. The `%1` in the `kill` command causes the shell to substitute the real process ID (PID) before invoking the `kill` command. If you leave the server running on port `9099`, and you attempt to start another on the same port, you will see something like this: