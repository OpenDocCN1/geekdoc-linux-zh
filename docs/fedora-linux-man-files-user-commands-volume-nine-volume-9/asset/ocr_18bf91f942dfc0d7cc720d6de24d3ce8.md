# **OPTIONS**

The anings of the available options are:

+   -  **\+, --append**
+       append received data to an existing file (ZMODEM, ASCII only).
+   -  **\-a, --ascii**
+       Convert files to `Unix` conventions by stripping carriage returns and all characters beginning with the first `Control Z` (`CP/M` end of file).
+   -  **\-b, --binary**
+       `Binary` (tell it like it is) file transfer override.
+   -  **\-B** `NUMBER`, **--bufsize** `NUMBER`
+       Buffer **NUMBER** bytes before writing to disk. `Default` is `32768`, which should be enough for most situations. If you have a slow machine or a bad disk interface or suffer from other hardware problems you might want to increase the buffersize. **\-1** or `auto` use a buffer large enough to buffer the whole file. Be careful with this options - things normally get worse, not better, if the machine starts to `swap`.
+   -  **\-c, --with-crc**
+       `XMODEM` only. Use `16` bit `CRC` (normally a `one` byte `checksum` is used).
+   -  **\-C, --allow-remote-commands**
+       allow remote command execution (**`insecure`**). This allows the sender to execute an arbitrary command through `system`() or `exec`(). Default is to disable this feature (?). This option is ignored if running in `restricted mode`.
+   -  **\-D, --null**
+       Output file data to `/dev/null` ; for testing. (`Unix` only)
+   -  **--delay-startup** `N`
+       Wait `N` seconds before doing anything.
+   -  **\-e, --escape**
+       Force sender to escape all control characters; normally `XON, XOFF, DLE, CR-@-CR`, and `Ctrl-X` are escaped.
+   -  **\-E, --rena**
+       Rena incoming file if target filena already exists. The new file na will have a dot and a nuer (`0...999`) appended.
+   -  **\-h, --help**
+       give help screen.
+   -  **\-m** `N`, **--min-bps** `N`
+       Stop transmission if `BPS-Rate` (`Bytes Per Second`) falls below `N` for a certain ti (see --min-bps-ti option).
+   -  **\-M** `N`, **--min-bps-ti**
+       Used together with --min-bps. `Default` is `120` (seconds).
+   -  **\-O, --disable-tiouts**
+       Disable read tiout handling code. This makes lrz hang if the sender does not send any more, but increases performance (a bit) and decreases system load (though reducing the nuer of system calls by about `50` percent).