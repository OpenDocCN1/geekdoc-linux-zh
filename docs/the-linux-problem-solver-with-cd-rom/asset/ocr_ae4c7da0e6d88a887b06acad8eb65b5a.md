connect command With a command, initializes the connection before PPP initiates on the remote side. Usually an invocation of the chat command—for example, connect '/usr/sbin/chat -v -f /etc/ppp/chat-isp'.

nodetach Normally, pppd acts as a real daemon and forks off into a background process while running. The nodetach option disables this forking off—handy for debugging, as it makes pppd interruptible immediately with CTRL-C.

mru number Defines the maximum receive unit (mru), which tells the remote server not to send any chunks of data larger than number bytes. The size you set depends on how fast your connection is; the default of 1500 bytes is fine for modem speeds such as 33.6k baud.

mtu number pppd won't transmit chunks of data higher than the number bytes you set here. (The default is 1500 bytes.) Tweak this value (usually by lowering it) when you're having difficulty uploading data onto a remote machine or when your connection seems slow (even if it's only via modem). (Note that the quality of phone lines and switches often limits the capacity for sending data back through the line.)

# PROBLEM 5

Symptom: Some programs cannot send or receive data at all.

Problem: mtu and mru too low.

Fix: You need to set the mtu and mru higher. In general, settings of lower than 1300 bytes will cause problems with many applications (like scp).

# PROBLEM 6

Symptom: Connection often hangs or drops. ARQ light on modem often blinks.

Problem: Poor switch or telephone line.

Fix: If you can't find a problem with the wiring in your building, you'll have to work with the phone company. Sometimes the problem is a poor connection to the building, but often the company's overloading the phone switch. If you notice a lot of static when you're using the voice phone, see if you can get the phone company to put you on a better switch.