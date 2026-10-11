# 144  Chapter 6: **Connectionless-Oriented Protocols**

The program shown in Listing 6.1 can now be described in detail that is more complete, as follows:

+   1.  Lines 20 to 27 form our simple error-handling function. Its purpose is to report an error, should it occur, and exit out of the program. Real applications would provide better error handling than this.
+   2.  Lines 49 to 55 choose a server address for this server program. If no command-line argument is provided, then the arbitrary address **127.0.0.23** is used. Note that this default address will work for you, even if you do not have any network cards installed.
+   3.  Lines 60 to 62 create a datagram socket. This causes a UDP protocol socket number to be assigned to variable s, when the **socket(2)** call is successful.
+   4.  Lines 68 to 77 form the address structure **adr\_inet** and establish the address structure length in variable **len\_inet**.
+   5.  Lines 84 to 88 bind the address established in step 4, to the socket s that was created in step 3.
+   6.  A loop begins in line 93.
+   7.  The maximum size of the receiving address buffer is computed in line 98 and assigned to variable **len\_inet**. The receiving address buffer will be the structure **adr\_clnt**.
+   8.  The function **recvfrom(2)** is called in line 99. This function call will block until the server receives a datagram. Upon return from this function, buffer **dgram** will contain the datagram, and variable **z** will contain the size of this datagram (or −1 if there was an error returned). The sender's socket address is returned in structure **adr\_clnt**, and variable **len\_inet** is set to the length of the address in **adr\_clnt**.
+   9.  If step 8 is successful, the variable **z** is the length of the datagram message that was received. Line 111 places a null byte at the end of the buffer, so that buffer **dgram[\]** may be treated as a null terminated C string.
+   10. Line 112 tests to see if the datagram contains the string `"QUIT"`. If so, this is a signal for the server to quit, and control breaks out of the loop in line 113.
+   11. The current date and time are fetched in lines 118 and 119.