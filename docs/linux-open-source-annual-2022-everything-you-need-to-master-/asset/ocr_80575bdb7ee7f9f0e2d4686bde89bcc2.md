![](bbox=[0.06, 0.11, 0.81, 0.43])

> On this laptop, -march=native gives a noticeable boost to almost all benchmarks. -Ofast gives a small speedup to some, and removing -g has little effect.

short for gigaflops, or 'billion floating point operations' (where a 'floating point operation' is any operation such as addition or multiplication done on a number with a decimal point). Since most supercomputers are used to crunch numbers for science and engineering applications, this gives a pretty good comparator between different machines.

To activate the SSH server, run:
```bash
$ sudo systemctl start ssh
```
On Red Hat-derived distributions, this will be `sshd` instead of `ssh`. Then on each machine in turn, generate an SSH key by running
```bash
$ ssh-keygen
```

# Get parallel!

So far this is only using a single core of your CPU. Since you'll be hard-pressed to find a computer with only one core in 2019 (John's *Eee PC—Ed*) a good next step is to run using every core in your machine, to get the highest number you can. To find out how many cores your machine has, you can check the specs, or you can look in `lproc/cpuinfo` (if your CPU has hyper-threading, you'll need to divide by two, since `Open MPI` doesn't believe that those are real cores). Put the number you get in place of the 1 in the above command to run on all cores. For example, for a six-core workstation, run:
```bash
$ ./sombrero.sh -n 6 -s small
```

It's worth noting that because of the particular problem Sombrero is based on, it can only test a number of cores that is divisible only by 2 and 3. For example, 6 (2 × 3), 24 (2 × 2 × 2 × 3), or 32 (2 × 2 × 2 × 2 × 2) will work, but 10 (2 × 5) or 14 (2 × 7) won't work, and will give you an error.

Now you've successfully brought your entire machine to a halt, what about doing the same with your entire network? If you have more than one Linux machine joined by a network, you can try running Sombrero across every machine you have access to, forming a makeshift Beowulf cluster. First go, follow the instructions up to now for every computer that you want to participate. This will check that Sombrero works on each machine individually, and also set up the executable so that `Open MPI` can find it on each machine. Next, you need to configure SSH so you can log in from one machine to another without a password.

and pressing Return three times. Once this is done, you can copy the key to your other computers with
```bash
$ ssh-copy-id destination_machine
```

where `destination_machine` is the hostname or IP address of the machine to copy to. When prompted, enter your password for the destination machine to let the copy happen. If you have two computers you'll need to do this twice.

# » WHAT IS A SUPERCOMPUTER?

A modern supercomputer isn't too unlike a home or office network. A bunch of Linux servers (or nodes), often using Intel processors and mounted in racks, can all operate independently, but sit on a common network. In the fastest supercomputers, each server has one or more GPUs installed to perform the heavy grunt of the computation. Red Hat Linux is the most common distribution used, with Debian-derived distributions being more of a rarity.

While a typical Ethernet connection may be used for managing the nodes and logging into them, they are also connected together by an ultra high-speed interconnect such as Infiniband or Omnipath. The nodes need to work cooperatively on large problems, and don't want to sit idle waiting for data to arrive, so slarging the network layout is a crucial part of designing a supercomputer. While most machines will use a relatively familiar hierarchy of switches, some machines targeting specific applications will design the network around that, giving exotic shapes like dragonflies and six-dimensional toruses!

Intel CPUs will of the high-end server varieties, since this gives a much higher number of cores per node: current generation chips give up to 24 cores on a single chip, compared to eight on the highest-end Core i9. GPUs will be computationally-focused NVIDIA Tesla cards — often with no display output at all.

> QUICK TIP
> 
> If you're running on a Raspberry Pi, even the small test is too big to fit into the system's 1GB of RAM. You can specify a custom size, try -l 16x12x12x12.