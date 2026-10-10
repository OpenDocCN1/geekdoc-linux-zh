# Enabling Common TCP Services

**TABLE 4.7**
**FTP Protocol (continued)**

| DESCRIPTION | PROTOCOL | REMOTE ADDRESS | REMOTE PORT | LOCAL IN/OUT | LOCAL ADDRESS | LOCAL PORT | TCP FLAG |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| Local client port data channel response | TCP | ANYWHERE | 20 | Out | IPADDR | 1024:65535 | ACK |
| Local client passive data channel request | TCP | ANYWHERE | 1024:65535 | Out | IPADDR | 1024:65535 | Any |
| Remote server passive data channel response | TCP | ANYWHERE | 1024:65535 | In | IPADDR | 1024:65535 | ACK |
| Remote client request | TCP | ANYWHERE | 1024:65535 | In | IPADDR | 21 | Any |
| Local server response | TCP | ANYWHERE | 1024:65535 | Out | IPADDR | 21 | ACK |
| Local server port data channel response | TCP | ANYWHERE | 1024:65535 | Out | IPADDR | 20 | Any |
| Remote client port data channel response | TCP | ANYWHERE | 1024:65535 | In | IPADDR | 20 | ACK |
| Remote client passive data channel request | TCP | ANYWHERE | 1024:65535 | In | IPADDR | 1024:65535 | Any |
| Local server passive data channel response | TCP | ANYWHERE | 1024:65535 | Out | IPADDR | 1024:65535 | ACK |

FTP deviates from this standard TCP, client/server communication model. FTP relies on two separate connections, one for the control or command stream, and one for passing the data files and other information, such as directory listings. The control stream is carried over a traditional TCP connection. The client binds to a high, unprivileged port, and sends a connection request to the FTP server, which is bound to port **21**. This connection is used to pass commands.