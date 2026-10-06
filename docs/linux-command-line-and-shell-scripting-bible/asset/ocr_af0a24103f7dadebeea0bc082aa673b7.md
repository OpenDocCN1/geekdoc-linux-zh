# Advanced Topics

This command also blocks execution of script until it receives data from the client. This could be a bad thing if the client has lost connection to the network. To prevent this problem, you can use the -t option in the read line to specify a timeout value (in seconds). If the server doesn't receive data from the client in the timeout period, it continues on.

If the server receives data from the client, it displays the data on STDOUT, then sends it back to the client. If the data is equal to the text string exit, the server exits the loop, and uses the -c parameter in ztcp to close both the client's file descriptor, and the listening port's file descriptor. If you prefer to have your server listen for another connection, after you close the client's file descriptor you can loop back to waiting to accept a new connection.

# The client program

Here's the code for the client shell program:

```
% cat client
#!/bin/zsh
# zsh TCP client program
zmodload zsh/net/tcp

ztcp localhost 5150
hostfd=$REPLY

read line < $hostfd
echo $line

while [ 1 ]
do
  echo -n "Enter text: "
  read phrase
  echo Sending $phrase to remote...
  echo $phrase > $hostfd
  if [[ $phrase = "exit" ]]
  then
    break
  fi
  read line < $hostfd
  echo "* Received: $line"
done
ztcp -c $hostfd
%
```

The client program must specify the IP address (or hostname) of the system server program is running on, and the proper TCP port number the server is listening to. When the server accepts the connection, the ztcp program sets the file descriptor for the connection and saves the value in the $REPLY variable. The client program reads the server's welcome message, then displays it:

```
read line < $hostfd
echo $line
```