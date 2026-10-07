# Managing Printing Services

Printing services and job requests are handled by the lpd daemon, started by the /etc/rc.d/init.d/lpd startup script, which looks like this (in the part):

```
start () {
  echo -n $'Starting $prog: ""
  # Is this a printconf system?
  if [[ -x /usr/sbin/printconf-backend ]]; then
    run printconf-backend to rebuild printcap and spools
    if ! /usr/sbin/printconf-backend; then
      # If the backend fails, we dont start no printers defined
      echo -n "No Printers Defined"
      echo_success
    echo
    return 0
  fi
fi
```

Note that all the script is shown here. However, as you can see, the script first reports that the service is starting. Next, an associated command to the Red Hat printconf utility is used to check for the existence of your system's /etc/printcap database. The script starts the lpd daemon, which runs in the background as a process, waiting for any files to appear under a defined printer's directory under the /var/pool/lpd directory.

After defining a printer, you can use one or more traditional line printer spooler utilities to control printing services, manage printing (or print jobs), and enable, disable, or authorize remote printing services (see the section "Printing Tools" later in this chapter).

Table 12.1 contains a partial list of related printing commands and drivers included with Red Hat Linux.

# TABLE 12.1 Print-related Commands and Drivers

| Name | Description |
| --- | --- |
| a2ps | Formats text files for PostScript printing |
| dvi[lj,l4,l2p,l4] | Converts TeX D files to specific PCL format |
| encscript | Converts text files to PostScript |
| escputil | Epson Stylus inkjet printer utility |
| grolbp | groff driver for Canon LBP-4 and LBP-8 laser printers |
| gs | The Ghostscript interpreter |
| gsbj[dj500, lp] | Ghostscript Bubblejet printer drivers |
| gsdj[dj500,lj,lp] | Ghostscript Deskjet printer drivers |
| lpc | Printer control utility |
| lpd | Printing spooling daemon |
| lpf | General printer filter |