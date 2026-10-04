# 4.1 Pop Client

```
puts "Received: $line"
}
# send the user name
# Note that the socket can be used for both input and output
puts $popClient "user $popLoginID"
# The socket is buffered by default. Thus we need to
# either fconfigure the socket to be non-buffered, or
# force the buffer to be sent with a flush command.
flush $popClient
# Receive the password prompt:
# +OK Password required for popclient.
set response [gets $popClient]
if {[string match "+OK**" $response] == 0} {
    puts "ERROR: Did not get expected '+OK' prompt"
    puts "Received: $response"
}
# Send Password
puts $popClient "pass $popPasswd"
flush $popClient
# Receive the message count:
# +OK popclient has 0 messages (0 octets).
set message [gets $popClient]
if {[string match "+OK**" $message]} {
    puts "ERROR: Did not get expected '+OK' prompt"
    puts "Received: $message"
}
puts [string range $message 3 end]
# Script Output
popclient has 2 messages (2069 octets).
```