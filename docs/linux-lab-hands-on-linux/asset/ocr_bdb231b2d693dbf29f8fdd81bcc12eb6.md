```
    \append messages_seen \$message_id
\ns trace-annotate "\'\$node_node-addr\' sending message \$message_id" 
$Self sendto $size "$message_id:$data" 1 $port
}
# attach a new Agent/MessagePassing/Flooding to each node on port
\$MESSAGE_PORT
for {set i 0} {\$i < 3} {incr i} {
    set a($i) [new Agent/MessagePassing/Flooding]
    \$node_($i) attach $a($i) \$MESSAGE_PORT
    $a($i) set messages_seen {} 
}

\$ns at 0.1 "\$a(0) send_message 500 1 {first_message} \$MESSAGE_PORT"
\$ns at 0.1 "\$a(2) send_message 500 2 {second_message} \$MESSAGE_PORT"

\$ns at 0.8 "\$a(0) send_message 500 5 {fifth_message} \$MESSAGE_PORT"
\$ns at 0.8 "\$a(2) send_message 500 6 {sixth_message} \$MESSAGE_PORT"

\$ns at 1.3 "\$a(2) send_message 500 15 {fifteenth_message} \$MESSAGE_PORT"
\$ns at 1.3 "\$a(0) send_message 500 16 {sixteenth_message} \$MESSAGE_PORT"
for {set i 0} {\$i < 3} {incr i} {
    \$ns initial_node_pos \$node_(\$i) 30
    \$ns at 20.0 "\$node_($i) reset";
}

\$ns at 20.0 "finish"
\$ns at 20.1 "puts '\\'NS EXITING...\'\'; \$ns halt"

#INSERT ANNOTATIONS HERE

proc finish {} {
    global ns f nf val
    \$ns flush-trace
    close $f
    close $nf
}

puts "Starting Simulation..."

\$ns run
```