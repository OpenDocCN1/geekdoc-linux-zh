WAN interface. For simplicity, the firewall on MULTISERVER03 also allows inbound TCP port 3389, meaning we are able to log in over RDP directly.

| WAN | DMZ | INTERNAL |
| --- | --- | --- |
| ![image](image_url) | ![image](image_url) | ![image](image_url) |
| KALI_MACHINE | MULTISERVER03 | PGDATABASE01 |
| [x] inbound | [x] inbound | MIRSHARES |
| [x] outbound | [x] outbound | |
| | | ![image](image_url) |
| | | PGDATABASE01-1 |

Figure 25: The network setup for this scenario

We want to SSH into PGDATABASE01 directly from our Kali machine. To do this, we need to create a port forward on MULTISERVER03 that will listen on the WAN interface and forward packets to the SSH port on PGDATABASE01.

> The proxy subcontext of the net interface command requires administrative privileges to make any changes. This means that in most cases we will need to take UAC into account. In this example, we're running it in a shell over RDP using an account with administrator privileges, so UAC is not a concern. However, we should bear in mind that UAC may be a stumbling block in other setups.

To start setting up a port forward, let's RDP directly into MULTISERVER03 from our Kali machine using xfreerdp.

```
kalikali~$ xfreerdp -u:admin /p:psssword /v:192.168.50.64
[07:08:02:2577] [265164:265165] [WARN][com.freerdp.crypto] - Certificate verification failure - 'self signed' certificate (18*) at stack position 0
[07:08:02:5777] [265164:265165] [WARN][com.freerdp.crypto] - CN = MULTISERVER03
[07:08:03:6851] [265164:265165] [ERROR][com.winpr.time] - Unable to find a match for unix time: US/Eastern
[07:08:03:8486] [265164:265165] [INFO][com.freerdp.gdi] - Local framebuffer format PIXEL_FORMAT_BGRX32
[07:08:03:8861] [265164:265165] [INFO][com.freerdp.gdi] - Remote framebuffer format PIXEL_FORMAT_BGRX32
[07:08:03:9480] [265164:265165] [INFO][com.freerdp.channels.rdpsns.client] - [static] Loaded fake backend for rpdsnd
[07:08:03:9480] [265164:265165] [INFO][com.freerdp.channels.drdynvnc.client] - Loading Dynamic Virtual channel rdpgfx
```