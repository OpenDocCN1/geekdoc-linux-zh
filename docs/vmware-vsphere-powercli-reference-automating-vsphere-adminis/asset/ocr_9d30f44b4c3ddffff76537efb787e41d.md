So far, good. Next, add a distributed virtual port group (DVPG) for the VDS you created in Listing 3.11. Listing 3.12 will create the following DVPG:

+   - Name: dvPG01

+   - Number of ports: 256

+   - VLAN: 42

# Listing 3.12 Creating a new DVPG

```
New-VDSPortgroup -Name 'dvPG01' -VDSSwitch $VDSwitch -NumPorts 256 -VlanId 42
```

You could configure additional information on the VDS and DVPG, but let's skip to the end and reveal the true power here. The code in Listing 3.13 will create a complete VDS that consists of the following:

PROD01-VDS02

+   - Prod01 datacenter

+   - 6 uplinks

+   - Cisco Discovery Protocol (CDP) enabled, and set to Both

+   - Administrator: Joe Bloggs

+   - Administrator Contact: Joe.Bloggs@example.com

+   - Network I/O control enabled

+   - VDS02-VLAN22

+   - 256 ports

+   - VLAN: 22

+   - Enable Promiscuous mode, MAC Address changes, and forged transmits

+   - Uplink ports Active 2, 4; Standby 3

+   - VDS02-Trunk01

+   - 128 ports

+   - VLANs: 7, 19, 25 – 28

+   - Uplink ports Active 2, 4; Standby 3