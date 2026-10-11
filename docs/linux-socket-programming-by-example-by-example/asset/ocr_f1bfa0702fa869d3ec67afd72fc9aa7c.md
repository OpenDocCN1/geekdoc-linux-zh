```
59:      option = sizeof rcvbuf;
60:      z = getsockopt(s, SOL_SOCKET, SO_RCVBUF,
             &rcvbuf, &option);
62:      if ( z )
63:          bail(*getsockopt(s, SOL_SOCKET,
             "SO_RCVBUF");
65:      
66:      assert(option == sizeof rcvbuf);
67:      
68:      /*
69:       * Report the buffer sizes:
70:       */
71:      printf("Socket s: %d\n", s);
72:      printf(" Send buf: %d bytes\n",
             sndbuf);
74:      printf(" Recv buf: %d bytes\n",
             rcvbuf);
76:      
77:      close(s);
78:      return 0;
79:      }
```

The getsockopt(2) steps used were as follows:

+   1. The options SO_SNDBUF and SO_RCVBUF are received into an int data type. Consequently, storage for these values was declared in lines 33 and 34.

+   2. The getsockopt(2) function requires an option length argument that acts as both an input value and a return value. Storage for this was allocated in line 35 and named option. Note that the data type for this variable is socklen_t.

+   3. A socket for testing purposes is created in line 40.

+   4. The length of the receiving option buffer sndbuf is established in variable option (line 47).

+   5. The option is fetched by calling getsockopt(2) in line 48. The socket level was SOL_SOCKET and the option name was specified as SO_SNDBUF. Note the pointer to sndbuf was given as the receiving buffer.

+   6. The length of the result returned in sndbuf is placed into variable option by the function getsockopt(2). Line 54 uses the assert(3) macro to ensure that it matches the return length that was expected.

+   7. Lines 59 to 66 repeat the process for the option SO_RCVBUF into variable rcvbuf.

+   8. Lines 71 to 75 report the socket file descriptor, and the corresponding buffer sizes that were retrieved.