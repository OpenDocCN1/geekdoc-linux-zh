tion you can define behavior after different split-brain scenarios. The after-sb-0pri section defines what to do when both nodes are listed as secondary after a split brain. The default is to use the data from the node that was the primary before the split brain occurred. The next option sets what to do if one of the nodes was the primary after the split brain. The default is consensus. With consensus, the secondary’s data will be discarded if the after-sb-0pri setting would also destroy it. Otherwise the nodes will disconnect from each other so you can decide which node will overwrite the other. The final after-sb-2pri option defines what to do if both nodes think they are the primary after a split brain. Here DRBD will disconnect the two nodes from each other so you can decide how to proceed. Check out the sample drbd.conf file for a full list of other options you can use for this section.

NOTE I could have condensed the configuration file quite a bit since both nodes will use the same type of metadisk, disk, and drive settings. Here’s an example of a condensed drbd.conf:

```
global {
    usage-count no;
}

common {
    protocol C;
}

resource r0 {
    device    /dev/drbd1;
    disk      /dev/sdb1;
    meta-disk internal;
    on node1 {
        address  192.168.10.1:7789;
    }
    on node2 {
        address  192.168.10.2:7789;
    }
    net {
        after-sb-0pri  discard-younger-primary;
        after-sb-1pri  consensus;
        after-sb-2pri  disconnect;
    }
}
```