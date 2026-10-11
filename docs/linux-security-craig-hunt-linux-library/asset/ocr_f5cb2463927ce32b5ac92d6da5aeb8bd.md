```
$ ( K I L L ) - H U P $( P I D )
 ;;
' -1')
$ ( K I L L ) -1$( P I D )
 ;;
*)
$ ( K I L L ) $ ( S I G N A L ) - $ ( P I D )
rm $F I L E
 ;;
esac
```

Note that the Linux utility killall generally works the same way as stopsocks, but it lacks the ability to stop a specific SOCKS5 server in cases where you're running multiple servers on different TCP ports. This can only be easily accomplished with the -p option of the stopsocks command.

**Table 10.8 stopsocks Script Command-Line Options**  
| **Option** | **Description** |
|---|---|
| -INT | Gracefully stops the SOCKS5 daemon. |
| -KILL | Abruptly stops operation of the SOCKS5 daemon. |
| -HUP | Forces the SOCKS5 daemon to re-read its configuration file. |
| [-p=port] | Stops a server running on the specified port. |
| [pid] | Process ID of server. |

To stop the server on PID 1245, use the following command:

```
[ramon]$ sudo /usr/local/bin/socks5 -INT 1245
```

To force the server on port 1080 to read its configuration, use the following command:

```
[ramon]$ sudo /usr/local/bin/socks5 -HUP -p 1080
```

# The runsocks Script

The SOCKS5 distribution comes with a compile option to build a dynamically linked library (/usr/local/lib/libsocks5_sh.so) that can be used by native Linux client applications in conjunction with a SOCKS5 server. The script /usr/local/bin/