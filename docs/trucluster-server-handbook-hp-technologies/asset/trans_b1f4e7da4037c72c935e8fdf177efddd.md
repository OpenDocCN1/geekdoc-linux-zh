

You entered the following information:

Cluster name:                              babylon5.dec.com
Cluster alias IP Address:                  192.168.0.70
Clusterwide root partition:                dsk6a
Clusterwide usr partition:                 dsk6g
Clusterwide var partition:                 dsk6h
Clusterwide il8n partition:                Not-Applicable
Quorum disk device:                        dsk5
Number of votes assigned to the quorum disk: 1
First member's member ID:                  1
Number of votes assigned to this member:   1
First member's boot disk:                  dsk1
First member's virtual cluster interconnect device name: ics0
First member's virtual cluster interconnect IP name:     molari-ics0
First member's virtual cluster interconnect IP address:  10.0.0.1
First member's physical cluster interconnect devices     alt0
First member's NetRAIN device name        Not-Applicable
First member's physical cluster interconnect IP address   10.1.0.1

If you want to change any of the above information, answer 'n' to the following prompt. You will then be given an opportunity to change your selections.

Do you want to continue to create the cluster? [yes]:

Now that we are satisfied with all our entries and it matches our plan for the creation of our cluster, from the Cluster Preparation Worksheet and Checklist, we are ready to configure the cluster.

## 10.4.1.11 Configuring the Cluster

As we have already provided the clu_create software and all the inputs required to create a single-node cluster, let's see what happens during the actual configuration and creation of the cluster.

First, the member disk and the quorum disk are labeled, and the cnx partition on each is initialized.

```
Creating required disk labels.
Creating disk label on member disk : dsk1
Initializing cnx partition on member disk : dsk1h
Creating disk label on quorum disk : dsk5
Initializing cnx partition on quorum disk : dsk5h
```

Next, the AdvFS domains are created for all our system level file systems and for the first cluster member. These AdvFS domains are cluster_root, cluster_usr, cluster_var, and finally, the first cluster member's boot_partition (root1_domain).

- This is the output from the configuration using Memory Channel as a cluster interconnect.

```
Modifying configuration files required for cluster operation:
Creating /etc/fstab file.
Configuring cluster alias.
Updating /etc/hosts - adding IP address '192.168.0.70' and hostname 'babylon5.dec.com'
Updating member-specific /etc/inittab file with 'cms' entry.
Updating /etc/hosts - adding IP address '10.0.0.1' and hostname 'molari-ics0'
Updating /etc/rc.config file.
Updating /etc/sysconfigtab file.
Retrieving cluster_root major and minor device numbers.
Creating cluster device file CDSLS.
Updating /.rhosts - adding hostname 'babylon5.dec.com'
Updating /etc/hosts.equiv - adding hostname 'babylon5.dec.com'
Updating /.rhosts - adding hostname 'molari-ics0'
Updating /etc/hosts.equiv - adding hostname 'molari-ics0'
Updating /etc/ifaccess.conf - adding deny entry for 'ee0'
Updating /etc/ifaccess.conf - adding deny entry for 's10'
Finished updating member1-specific area.
```

- This is the output from a configuration using Ethernet LAN as the cluster interconnect.

```
Modifying configuration files required for cluster operation:
Creating /etc/fstab file.
Configuring cluster alias.
Updating /etc/hosts - adding IP address '192.168.0.70' and hostname 'babylon5.dec.com'
Updating member-specific /etc/inittab file with 'cms' entry.
Updating /etc/hosts - adding IP address '10.0.0.1' and hostname 'molari-ics0'
Updating /etc/hosts - adding IP address '10.1.0.1' and hostname 'member1-icstcp0'
Updating /etc/rc.config file.
Updating /etc/sysconfigtab file.
Retrieving cluster_root major and minor device numbers.
Creating cluster device file CDSLS.
Updating /.rhosts - adding hostname 'babylon5.dec.com'
Updating /etc/hosts.equiv - adding hostname 'babylon5.dec.com'
Updating /.rhosts - adding hostname 'molari-ics0'
Updating /etc/hosts.equiv - adding hostname 'molari-ics0'
Updating /.rhosts - adding hostname 'member1-icstcp0'
Updating /etc/hosts.equiv - adding hostname 'member1-icstcp0'
Updating /etc/ifaccess.conf - adding deny entry for 'ee0'
Updating /etc/ifaccess.conf - adding deny entry for 's10'
Finished updating member1-specific area.
```

