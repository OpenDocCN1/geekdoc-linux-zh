
# Linux Lab: Hands on Linux

## Chapter Overview

Linux Lab: Hands on Linux is a perfect guide for all those people who want to master Linux. This unique book provides step-by-step practical tutorials on different aspects of Linux in easy-to-understand language. Ready-to-use commands and code snippets along with descriptive illustrations are among many of the value added features of this book.

## The Book Covers

- **INSTALLATION OF LINUX:** Normal Installation with Dual Boot procedure and Network based Installation
- **LINUX SYSTEM ADMINISTRATION:** User Administration, Process Management, Memory Management, File System Management, Disk Management, Installation of Software, working with Editors and Backup and Restore
- **LINUX NETWORK ADMINISTRATION:** Configuring TCP/IP Addresses, Configuring NIC, Setting Default Gateway, Hostname Configuration, GUI Configuration Tools, Networking Commands and Utilities
- **LINUX SERVER ADMINISTRATION:** Installation and Configuration of TELNET, SSH, FTP, Apache Web Server, NFS Server, DNS, DHCP, SQUID proxy
- **DATABASE MANAGEMENT:** Installing MySQL, Configuring MySQL, Adding Data to MySQL Database Table, Sorting Data, Updating and Deleting Records, Taking Backup of Database
- **KERNEL CONFIGURATION:** Different Kernel Modules, Kernel Version Naming Conventions, Kernel Compilation, Patching Kernel, and Booting the Custom Kernel
- **LINUX ENGINEERING TOOLS:** Installing and Using Network Simulator, Running TCL Scripts on NS2, and Installing and Using SCILAB
- **PROGRAMMING IN LINUX:** Shell Scripting, Java Programming in Linux, C Programming in Linux, and C++ Programming in Linux

## About the Authors

**DAYANAND AMBAWADE** is an Asst. Professor in Sardar Patel Institute of Technology at Mumbai. He received a M.Tech. from Indian Institute of Technology, Bombay. He has 12 years academic and industry experience. His research interest includes Computer Networks & Security, Mobile Wireless Networks & Open Source Software (OSS). He has delivered and conducted seminars/workshop at various STTP and Conferences. He has published papers in International Conferences. He is a fellow of IETE, member of IEEE and LM-ISTE.

**DEVEN N. SHAH** is working with Sardar Patel Institute of Technology, Mumbai. He has 14 years of academic and industry experience. He has worked as a technical consultant in various computer institutes. He has received Best Faculty award from IBM US in 2007. He has also been nominated for the Faculty award for the year 2008-09. Presently, he is working with a France-based university for a joint research program; and is pursuing research on Service Oriented Architecture.

**CATEGORY:**  
**Engineering**  

**USER LEVEL:**  
**Beginner to Intermediate**

![](img/f3b9cff79e19317416c12eaf5ded7245_289_0.png)

**PUBLISHED BY:**

dreamtech 

19-A, Ansari Road, Daryaganj, New Delhi-110002
Tel: 91-11-23284212, 23243075
Fax: 91-11-23264078
Email: feedback@dreamtechpress.com
www.dreamtechpress.com

![](img/f3b9cff79e19317416c12eaf5ded7245_289_1.png)

## Appendix A: NS2 Simulation Script

```tcl
# FOR ANY DIRECT, INDIRECT, INCIDENTAL, SPECIAL, EXEMPLARY, OR CONSEQUENTIAL
# DAMAGES (INCLUDING, BUT NOT LIMITED TO, PROCUREMENT OF SUBSTITUTE GOODS
# OR SERVICES; LOSS OF USE, DATA, OR PROFITS; OR BUSINESS INTERRUPTION)
# HOWEVER CAUSED AND ON ANY THEORY OF LIABILITY, WHETHER IN CONTRACT, STRICT
# LIABILITY, OR TORT (INCLUDING NEGLIGENCE OR OTHERWISE) ARISING IN ANY WAY
# OUT OF THE USE OF THIS SOFTWARE, EVEN IF ADVISED OF THE POSSIBILITY OF
# SUCH DAMAGE.
#

# Mac/simple set bandwidth_ 1Mb

set MESSAGE_PORT 42
set BROADCAST_ADDR -1

#set val(chan)        Channel/WirelessChannel     ;#Channel Type
set val(prop)         Propagation/TwoRayGround    ;# radio-propagation model
set val(netif)        Phy/WirelessPhy             ;# network interface type

set val(mac)          Mac/802_11                  ;# MAC type
#set val(mac)         Mac
set val(mac)          Mac/Simple                  ;# MAC type

set val(ifq)          Queue/DropTail/PriQueue      ;# interface queue type
set val(ll)           LL                           ;# link layer type
set val(ant)          Antenna/OmniAntenna          ;# antenna model
set val(ifqlen)       32768                        ;# max packet in ifq

set val(rp) DummyAgent
set ns [new Simulator]

set f [open rts-cts-data-ack.tr w]
$ns trace-all $f
$ns eventtrace-all
set nf [open rts-cts-data-ack-temp.nam w]
$ns namtrace-all-wireless $nf 700 200

# set up topology object
set topo            [new Topography]

$topo load_flatgrid 700 200

$ns color 3 green;
$ns color 8 red;
$ns color 1 black;
$ns color 7 purple;
$ns color 6 tan;
$ns color 2 orange;

#
# Create God
#
create-god 3

#set mac0 [new Mac/802_11]

$ns node-config -adhocRouting ${val(rp)} \
        -lltype ${val(ll)} \
        -macType ${val(mac)} \
        -ifqType ${val(ifq)} \
        -ifqLen ${val(ifqlen)} \
        -antType ${val(ant)} \
        -propType ${val(prop)} \
        -phyType ${val(netif)} \
        -channelType Channel/WirelessChannel \
        -topoInstance $topo \
        -agentTrace ON \
        -routerTrace OFF \
        -macTrace ON \
        -movementTrace OFF

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
    lappend messages_seen $message_id
    $ns trace-annotate "$node_ [node_ node-addr] sending message $message_id" 
    $self sendto $size "$message_id:$data" 1 $port
}

# attach a new Agent/MessagePassing/Flooding to each node on port MESSAGE_PORT
for {set i 0} {$i < 3} {incr i} {
    set a($i) [new Agent/MessagePassing/Flooding]
    $node_($i) attach $a($i) $MESSAGE_PORT
    $a($i) set messages_seen {} 
}

$ns at 0.1 "$a(0) send_message 500 1 {first_message} $MESSAGE_PORT"
$ns at 0.1 "$a(2) send_message 500 2 {second_message} $MESSAGE_PORT"

$ns at 0.8 "$a(0) send_message 500 5 {fifth_message} $MESSAGE_PORT"
$ns at 0.8 "$a(2) send_message 500 6 {sixth_message} $MESSAGE_PORT"

$ns at 1.3 "$a(2) send_message 500 15 {fifteenth_message} $MESSAGE_PORT"
$ns at 1.3 "$a(0) send_message 500 16 {sixteenth_message} $MESSAGE_PORT"

for {set i 0} {$i < 3} {incr i} {
    $ns initial_node_pos $node_($i) 30
    $ns at 20.0 "$node_($i) reset";
}

$ns at 20.0 "finish"
$ns at 20.1 "puts '\nNS EXITING...'; $ns halt"

#INSERT ANNOTATIONS HERE

proc finish {} {
    global ns f nf val
    $ns flush-trace
    close $f
    close $nf
}

puts "Starting Simulation..."

$ns run
```
