
it to another hard drive? Sure! Stack an encryption module on top of your hard drive and then stack the drive-mirroring module on top of that. You want to mirror that drive across the network? Add that GEOM class to the stack. This flexible modularity makes GEOM one of FreeBSD's most powerful features.

## GEOM Autoconfiguration

When FreeBSD finds a new storage device, either at boot or when you plug a new drive in, the GEOM subsystem checks the device for known formats, like a master boot record, a BSD disklabel, or other metadata. GEOM also checks for physical identifiers, such as the disk's serial number. This is called *tasting*.

When GEOM finds identifying information, it configures the device as that metadata dictates. If a disk's metadata says, “I'm part of a mirror called *garbage*, along with two other disks,” GEOM looks for the other disks and assembles the mirror. If GEOM can identify a storage device by format, label, or other information, it starts the device, fires up an instance of the GEOM class, makes the appropriate device nodes, and performs any other configuration it understands.

If GEOM can't identify any other metadata on the disk, such as on an unformatted and unpartitioned disk, GEOM creates the device node for the storage device and leaves it alone.

An instance of a GEOM class is called a *geom*. The gmirror(8) class makes disks mirror each other, but the specific pair of mirrored disks named *garbage* is a geom. Each disk in that mirror is also a geom.

## GEOM vs. Volume Managers

Traditional volume managers expect you to do things their way, whether that makes sense for your environment and hardware or not. If the volume manager says that you create an encrypted disk mirror by encrypting the individual drives and then mirroring on top of them, that's what you do. It might make more sense in your environment to mirror the drives and then encrypt them, but if that's not what the volume manager does, too bad. Worse, some volume managers make poor choices and then implement fixes sideways to minimize the consequences of those decisions.

GEOM differs from volume managers in that it assumes you know what you're doing. It gives you flexibility to arrange your storage in the manner that best fits your hardware and benefits your use case. GEOM classes let you easily insert new data transformations into your storage. You can't, say, add an encryption layer into your commercial volume manager.

Volume managers cover the most common cases for hardware that existed at the time they were conceived. As time passes, though, that most common case becomes increasingly uncommon. People continue to use volume managers long after the hardware they were designed for becomes obsolete. GEOM lets you evolve your designs with your hardware, environment, and application.

FreeBSD includes two software suites that look much like volume managers: gvinum(8) and ZFS. Vinum was the FreeBSD volume manager in the 1990s, and while gvinum(8) reimplements it as a GEOM class, its use is strongly discouraged. ZFS is very powerful, as we saw in Chapter 5, but it does have the "do it our way" ethos of a volume manager.

While you can theoretically stack GEOM modules forever, you must consider your hardware resources. Mirroring a busy disk across a network can require a dedicated network interface and an otherwise empty cross-connect cable. Encrypting and decrypting data eats processor time and memory. GEOM doesn't prevent you from thrashing your disks; it merely gives you new and interesting opportunities for doing so.

## Providers, Consumers, and Slicers

Individual geoms are either consumers, providers, or both.

- A *provider* offers services to another geom. If you're mirroring two hard drives, the geoms for the hard drive provide the disk to the mirror. A provider usually has a device node, such as `/dev/ada1p1`.

- A consumer uses the provider’s services. A disk-mirror geom consumes the underlying disk drives. The consumer part of a geom doesn’t need a device node.

- A geom can be both a provider and a consumer—indeed, every geom in the middle of a stack must be both. A disk-mirror geom consumes the underlying physical storage media, but it provides a mirrored disk for the filesystem to live on.

- FreeBSD treats all providers and consumers identically. A physical hard drive is just another provider, exactly like a mirror or encryption layer or import from the network. This characteristic lets you arbitrarily stack GEOM classes.

- A GEOM class that subdivides a class is called a slicer and is usually responsible for managing partitions. The GEOM class that handles master boot record (MBR) partitions is a slicer, as is the GUID Partition Table (GPT) class. We discussed both of these partitioning methods in Chapter 2, and we’ll go deeper into both in this chapter. Slicers must make sure that disk partitions don’t overlap and that the partitions conform to the rules of the partitioning scheme.

## GEOM Control Programs

Many GEOM classes have a control program that lets you administer the module or interrogate the device. Some widely used classes use geom(8), while other classes use programs like gmirror(8) or geli(8). The disk GEOM class talks to the physical storage media and provides consumers for upper layers. That’s a really commonly used class. Here, I interrogate a host to see what geoms of type disk it has and print out the information the disk offers the operating system.

```
$ geom disk list
1. Geom name: da0
   Providers:
   1. Name: da0
   2. Mediasize: 1000204886016 (932G)
   3. SectorSize: 512
   4. Mode: r2w2e3
   5. descr: ATA WDC WD1003FBYZ-0
   6. luname: ATA WDC WD1003FBYZ-01OFB0 WD-WCAW36478143
   7. lunit: 50014ee25e60dab5
   8. ident: WD-WCAW36478143
   9. rotationrate: 7200
   10. fwsectors: 63
   fwheads: 255
```

This hard drive provides a disk device called da0 ❶. The mediasize field gives its size in bytes and converts it to a more convenient 932GB ❷.

This disk claims to have a sector size of 512 bytes ❸. Many disks lie about their sector size. Check the drive manufacturer's documentation to determine the actual sector size. Drives might offer a Stripe size value of 4,096 to indicate that they're actually 4K drives.

A GEOM class's mode looks an awful lot like file permissions ❹, but it's really the number of GEOM classes reading from (r2) and writing to (w2) the device, plus the number of devices that have requested exclusive access to the device (e3).

The descr field ❺ offers the drive's model number.

The luname field ❻ gives the model number plus the serial number. Yes, it's a combination of the descr and ident fields. The hard drive really, really wants you to believe this is its name and identifier.

The lunit ❼ gives the logical-unit-number (LUN) identifier, which describes how this drive attaches to this host.

The disk's ident ❽ is the drive's serial number.

The rotationrate ❾ tells us how fast this drive spins. It's a 7,200 RPM disk. Nonspinning disks, like SSDs, have a rotationrate of 0.

The fwsectors and fwheads fields ❿ give us the drive geometry. These are examples of the lies mentioned in the beginning of this chapter. Even SSDs offer these values.

Some drives offer less information. Virtual disks offer almost no information, and anything they do say, you can't trust. (While the VM system might say this disk offers 32,212,254,720 512-byte sectors, who knows what the actual disk beneath the virtual disk has?)

## GEOM Device Nodes and Stacks

Many sysadmin tools expect to run on a disk or disk partition. Unix-like systems offer disks and partitions as device nodes. GEOM offers device nodes so that these tools remain compatible.

Most active GEOM modules have their own directory in `/dev`. Device nodes within that directory represent the current providers of that module. The directory is often, but not always, named after the GEOM module using it. For example, the gmirror(8) class uses `/dev/mirror`.

The directory name might be changed to avoid ambiguity or overlaps. The *glabel* (*GEOM label*) class uses `/dev/label`. The `/dev/gpt` directory contains the labels stored on GPT partitions, where `/dev/gptid` contains the numerical identifiers integral to GPT partitions.

Some classes don’t create a directory and instead piggyback on existing devices. The gnop(8) class creates a new node right next to the node it’s attached to but appends `.nop` to the end of the device name.

## Hard Disks, Partitions, and Schemes

While we discussed partitioning in Chapter 9, consider partitions from a disk drive perspective. The first possible SATA disk on our first SATA controller is called `/dev/ada0`. Subsequent disks are `/dev/ada1`, `/dev/ada2`, and so on. If you also have SAS disks, they’ll start their numbering over at 0.

Disks get further divided into *partitions*. Even average consumer-grade systems running Microsoft operating systems ship with multiple partitions on the hard drive. Sysadmins chop huge disk arrays into smaller, more manageable units with dedicated purposes—or perhaps they go the other way and merge multiple disks into one monster partition.

A *partitioning scheme* is the system for organizing partitions on a disk. The traditional master boot record (MBR) is one partitioning scheme. Old Apple and SPARC hardware have their own schemes. Today, the
