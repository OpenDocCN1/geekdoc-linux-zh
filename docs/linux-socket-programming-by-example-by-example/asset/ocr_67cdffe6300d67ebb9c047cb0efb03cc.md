+   - Setting Socket Options ... 310
+     - Applying the setsockopt(2) Function ... 311
+     - Retrieving the Socket Type (SO_TYPE) ... 315
+   - Setting the SO_REUSEADDR Option ... 317
+   - Setting the SO_LINGER Option ... 320
+   - Setting the SO_KEEPALIVE Option ... 323
+   - Setting the SO_BROADCAST Option ... 324
+   - Setting the SO_OOBINLINE Option ... 325
+   - Options SO_PASSCRED and SO_PEERCRED ... 326

# 13 Broadcasting with UDP ... 329

+   - Understanding Broadcast Addresses ... 330
+     - Broadcasting on 255.255.255.255 ... 330
+     - Enhancing the mkastr.c Subroutine ... 331
+   - Broadcasting from a Server ... 332
+   - Receiving Broadcasts ... 338
+   - Demonstrating the Broadcasts ... 342
+   - Broadcasting to a Network
+     - Starting Broadcasts ... 343
+     - Receiving Broadcasts ... 345
+     - Receiving Broadcasts from a Remote Host ... 345
+     - Troubleshooting Hints ... 346

# 14 Out-of-Band Data ... 349

+   - Defining Out-of-Band ... 350
+   - Understanding the Need for Out-of-Band Data ... 350
+   - Sockets and Out-of-Band Data ... 351
+   - Variations in Implementation ... 351
+   - Using Out-of-Band Data ... 353
+     - Writing Out-of-Band Data ... 353
+     - Reading Out-of-Band Data ... 354
+     - Understanding the Signal SIGURG ... 355
+     - Supporting Subprograms ... 356
+     - Receiving with the SIGURG Signal ... 359
+     - Sending Out-of-Band Data ... 362
+   - Testing the cobrecv and cobssend Programs ... 365