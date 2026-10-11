![](bbox=[0.08, 0.13, 0.92, 0.47])

```
icmp type='8'/>
      </rule>
      <rule action='accept' direction='in'
          priority='500'>
        <icmp type='0'/>
      </rule>
      <rule action='accept' direction='out'
          priority='500'>
        <udp dportstart='53'/>
      </rule>
      <rule action='accept' direction='out'
          priority='500'>
        <tcp/>
      </rule>
      <rule action='drop' direction='inout'
          priority='500'>
        <all/>
      </rule>
    </filter>
```

Save this file as `isolated_vm.xml` under `/etc/libvirt/nwfilter` on your RAWADA VDI server. Make it available. `virsh nwfilter-define isolated_vm`. Next, configure the virtual interface of all KALI domains with this new filter: `virsh edit YOUR_VM_NAME`. Add a reference to this filter within the `<interface>` description, as follows:

```
<filterref filter='isolated_vm'/>
```

Save it and voilà! From this moment on, any trainee will be able to connect to the internet and to any open port on the Web Security Dojo domain, but they won't have connectivity between them. Feel free to experiment with nwfilter rules (Again, see Resources).

From within your RAWADA VDI server, you can easily access any VM via its virtual serial console. This will help you recover access to the VM in case the SPICE connection stops working. This is described in the documentation (see Resources). However, don't forget to set up the VM accordingly by adding "console=ttyS0" to the grub.conf (/etc/default/grub on Debian-based systems) to make sure the system will spawn a serial console on /dev/ttyS0 every time it boots up.

# Connection via virtual serial console

# A bumpy road ahead of us ...

This is a great VDI project to start with. It is easy to install and set up and can be deployed quickly. However, it still has important flaws (as of this writing) that we hope will be fixed in upcoming releases. The database authentication mechanism lacks pseudorandom per-user salt generation; the SPICE protocol is not encrypted by default using a TLS channel (although, using TLS may decrease the VDI performance). A pseudorandom four-character temporary password is also generated to protect the remote SPICE connection to the desktop, which renders RAWADA VDI prone to brute-forcing attacks. But for our testing purposes it is perfect: you can start using it in order to deploy a whole pen-testing multi-user environment. And for all those flaws we just mentioned, well, there's always the possibility to create a git pull request! So, what are you waiting for? Time to get involved and get training!

> *Above Capture-the-flag scenarios can be deployed using RAWADA VDI within minutes; whether web pen-testing or binary exploitation, the sky is the limit!*