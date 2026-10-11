Example 10-23 Sample Log Entries. . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 215
Example 10-24 Use of Deny File as an Early Warning Mechanism. . . . . . . . . . . . . . . . . . . . . . . . . . . . 216
Example 10-25 Sample tcpdchk Output. . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 217
Example 10-26 Sample tcpdmatch Output. . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 217
Example 10-27 Using try-from. . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 218
Example 10-28 Output of make for Portmapper. . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 220
Example 10-29 Installing the Portmapper Binaries. . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 221
Example 10-30 Portmapper Start/Stop Script. . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 221
Example 10-31 Establishing the Portmapper Start/Stop Script for Run-Level Changes. . . . . . . . . . . . . 222
Example 10-32 Sample Entries for the Portmapper. . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 223
Example 10-33 Sample Log Output from portmap -v. . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 224
Example 10-34 Gracefully Terminating and Restarting portmap. . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 225
Example 10-35 Using configure for xinetd. . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 229
Example 10-36 Compiling and Linking xinetd. . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 229
Example 10-37 Output of make install for xinetd. . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 230
Example 10-38 Sample xinetd Start/Stop Script. . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 230
Example 10-39 Partial /etc/xinetd.conf File. . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 235
Example 10-40 Sample defaults Entry in /etc/xinetd.conf. . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 238
Example 10-41 Sample servers Entry. . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 239
Example 10-42 Example Output of servers Service. . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 239
Example 10-43 Sample services Entry in /etc/xinetd.conf. . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 240
Example 10-44 Output from a Query to the services Internal Service. . . . . . . . . . . . . . . . . . . . . . . . . . . . 241
Example 10-45 The xadm Entry. . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 241
Example 10-46 Using the xadm Service. . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 242
Example 10-47 Sample login Service Entry in /etc/xinetd.conf. . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 243
Example 10-48 Successful rlogin Attempt. . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 244
Example 10-49 Log Entries Associated with Example 10-48. . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 244
Example 10-50 Failed rlogin Attempts from Unauthorized Host. . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 245
Example 10-51 Log Entries Associated with Example 10-50. . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 246
Example 10-52 Binding Services to Specific Addresses. . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 247
Example 10-53 Use of redirect and bind in /etc/xinetd.conf. . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 248
Example 10-54 The Effect of redirect. . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 248
Example 10-55 Using TCP_wrappers in /etc/xinetd.conf. . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 249
Example 10-56 Log Record for a Hard Reconfiguration of xinetd. . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 252
Example 11-1 Installing SSH Using rpm. . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 265
Example 11-2 Representative /etc/ssh/sshd_config File. . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 274
Example 11-3 Sample Client-Side Configuration File. . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 280
Example 11-4 sshd Not Running on the Server. . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 283
Example 11-5 /etc/hosts.allow sshd Entry. . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 284
Example 11-6 Default Behavior for First Connection. . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 285
Example 11-7 $HOME/.ssh/known_hosts Entry for pluto. . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 285
Example 11-8 /etc/ssh/ssh_host_key.pub Entry for pluto on pluto. . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 285
Example 11-9 Warning Message Due to Changed Server Host Keys. . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 287
Example 11-10 Running make-ssh-known-hosts. . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 288