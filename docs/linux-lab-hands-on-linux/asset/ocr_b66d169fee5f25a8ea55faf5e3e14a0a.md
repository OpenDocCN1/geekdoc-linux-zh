```
–antType $val(ant) \n–propType $val(prop) \n–phyType $val(netF) \n–channelType Channel/WirelessChannel \n–topoinstance $topo \n–agentTrace ON \n–routerTrace OFF \n–macTrace ON \n–movementTrace OFF
for {set i 0} {$i < 3} {incr i} {
    set node_($i) [$ns node]
    $node_($i) random-motion 0
}
$node_(0) color black
$node_(1) color black
$node_(2) color black
$node_(0) set X_ 200.0
$node_(0) set Y_ 30.0
$node_(0) set Z_ 0.0
$node_(1) set X_ 330.0
$node_(1) set Y_ 150.0
$node_(1) set Z_ 0.0
$node_(2) set X_ 60.0
$node_(2) set Y_ 30.0
$node_(2) set Z_ 0.0
$ns at 0.6 "$node_(2) setdest 330.0 30.0 10000.0"
$ns at 1.1 "$node_(2) setdest 500.0 30.0 10000.0"
# subclass Agent/MessagePassing to make it do flooding
Class Agent/MessagePassing/Flooding -superclass Agent/MessagePassing
Agent/MessagePassing/Flooding instproc rec {source sport size data} {
    $self instvar messages_seen node_
    global ns
    # extract message ID from message
    set message_id [lindex [split $data ":"] 0]
    puts "$node_ [node_ node-addr] got message $message_id\n"
    if [lsearch $messages_seen $message_id] == -1 { 
        lappend messages_seen $message_id
        $ns trace-annotate "[$node_ node-addr] received ${data} from $source"
        $ns trace-annotate "[$node_ node-addr] sending message $message_id"
        $self sendto $size $data 1 $sport
    } else {
        $ns trace-annotate "[$node_ node-addr] received redundant message $message_id from $source"
    }
}
Agent/MessagePassing/Flooding instproc send_message {size message_id data port} {
    $self instvar messages_seen node_
    global ns MESSAGE_PORT
```