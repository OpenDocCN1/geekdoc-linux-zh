+   ■ W
+   Sending a reply

+   ■ K
+   Staying open as a keepalive process so it can send multiple files

+   ■ D
+   Performing DNS lookup

+   ■ C
+   Closing connection

+   ■ L
+   Logging

+   ■ G
+   Gracefully finishing

+   ■ I
+   Performing idle cleanup of worker

+   ■ . 
+   Open slot with no current process

Figure 8-1 shows a fairly idle web server with only one process in a K (keepalive) state and one process in a W (sending reply) state. If you are curious about what each of those processes were doing last, just scroll down the page to the table and find the process of the correct number in the scoreboard. So, for instance, the W process would be found as server 2-16. It’s not apparent in the screenshot, but that process was actually the response to the request for the server-status page itself. You will also notice a few _ (waiting for connection) processes in the scoreboard, which correspond to the number of processes Apache is configured to always have running to respond to new requests. The rest of the scoreboard is full of ., which symbolize slots where new process could go—basically the MaxClients setting (the maximum number of processes Apache will spawn).

What you will notice as you refresh this page is that the objects in the scoreboard should change during each request. This scoreboard is handy when you want to keep an eye on your web server; just continually refresh the page. During a spike, you are able to see new processes get spawned, switch