
## 选项

`qe-system-i386 dos.img -soundhw gus -parallel none`

或者：

`qe-system-i386 dos.img -device gus,irq=5`

或者其他未占用的 IRQ。

CS4231A 是用于 Windows Sound System 和 GUSMAX 产品中的芯片。

`disk_image` 是 IDE 硬盘 0 的原始硬盘映像。某些目标架构不需要硬盘映像。

标准选项：

- `-h`
  - 显示帮助并退出
- `-version`
  - 显示版本信息并退出
- `-machine [type=name],prop=value[,...]]`
  - 按 `name` 选择模拟的机器。使用 `-machine help` 列出可用的机器。
  - 支持的机器属性包括：
    - `accel=accels1[:accels2[...]]`
      - 用于启用加速器。根据目标架构，kvm、xen 或 tcg 可能可用。默认使用 tcg。如果指定了多个加速器，如果前一个初始化失败，则使用下一个。
    - `kernel_irqchip=on|off`
      - 在可用的情况下，为所选加速器启用内核 irqchip 支持。
    - `vmport=on|off|auto`
      - 启用 VMware I/O 端口模拟，用于 vmmouse 等。auto 表示根据 accel 选择值。对于 accel=xen，默认值为 off；否则默认值为 on。
    - `kvm_shadow_mem=size`
      - 定义 KVM 影子 MMU 的大小。
    - `dump-guest-core=on|off`
      - 在核心转储中包含来宾内存。默认为 on。
    - `mem-merge=on|off`
      - 启用或禁用内存合并支持。该功能（如果主机支持）会在虚拟机实例之间去重相同的内存页（默认启用）。
    - `iommu=on|off`
      - 启用或禁用模拟的 Intel IOMMU (VT-d) 支持。默认为 off。
    - `aes-key-wrap=on|off`
      - 在 s390-ccw 主机上启用或禁用 AES 密钥包装支持。此功能控制是否创建 AES 包装密钥以允许执行 AES 加密功能。默认为 on。
    - `dea-key-wrap=on|off`
      - 在 s390-ccw 主机上启用或禁用 DEA 密钥包装支持。此功能控制是否创建 DEA 包装密钥以允许执行 DEA 加密功能。默认为 on。
- `-cpu model`
  - 选择 CPU 模型（使用 `-cpu help` 查看列表和额外功能选择）
- `-smp [cpus=n],cores=cores],threads=threads],sockets=sockets],maxcpus=maxcpus]`
  - 模拟具有 n 个 CPU 的 SMP 系统。在 pc 目标上，最多支持 255 个 CPU。在 Sparc32 目标上，Linux 限制可用 CPU 的数量为 4。对于 pc 目标，可以指定每个套片的内核数、每个核心的线程数以及套片的总数。缺失的值将被计算。如果给出这三个值中的任意一个，则可以省略 CPU 总数 n。`maxcpus` 指定可热插拔 CPU 的最大数量。
- `-numa node[,mem=size][,cpus=cpu][-cpu][,,nodeid=node]`
- `-numa node[,memdev=id[,cpus=cpu[-cpu][,nodeid=node]]`
  - 模拟多节点 NUMA 系统。如果省略 mem、memdev 和 cpus，资源将被平均分配。此外，请注意 -numa 选项不会分配任何指定资源。也就是说，它只是将现有资源分配给 NUMA 节点。这意味着仍然必须使用 -m、-smp 选项分别分配 RAM 和 VCPUs，并且可能还需要使用 -object 来指定 memdev 子选项的内存后端。
  
  mem 和 memdev 是互斥的。此外，如果一个节点使用 memdev，那么所有节点都必须使用它。
- `-add-fd fd=fd[,set=set[,opaque=opaque]]`
  - 向文件描述符集添加一个文件描述符。有效选项包括：
    - fd: 此选项定义添加到 fd 集中的文件描述符的副本。该文件描述符不能是 stdin、stdout 或 stderr。
    - set: 此选项定义要添加文件描述符的 fd 集的 ID。
    - opaque: 此选项定义一个自由形式的字符串，可用于描述 fd。
  
  您可以使用来自 fd 集的预打开文件描述符来打开映像：
  `qe-system-i386 -add-fd fd=3,set=2,opaque="r:ddr:/path/to/file" -add-fd fd=4,set=2,opaque="r:ddnly:/path/to/file" -drive file=/dev/fdset/2,index=0,if=none,format=raw,id=hd0`
- `-set group.id.arg=value`
  - 设置组组中项目的解析参数值
- `-global driver.prop=value`
- `-global driver=driver,property=property,value=value`
  - 将驱动程序的属性 prop 的默认值设置为 value，例如：
  `qe-system-i386 -global ide-hd.physical_block_size=4096 -drive file=file,if=none,id=disk,physical_block_size=4096`
  
  特别是，您可以使用此功能为机器模型自动创建的设备设置驱动程序属性。如果要创建一个未自动创建的设备并为其设置属性，请使用 `-device`。
  
  `-global driver.prop=value` 是 `-global driver=driver,property=prop,value=value` 的简写形式。长格式语法在 driver 包含点号时也能正常工作。
- `-boot [order=drives][,once=drives][,menu=on|off][,splash=sp_name][,splash-time=sp_time] [,reboot-timeout=rb_timeout][,strict=on|off]`
  - 指定启动顺序 drives 作为驱动器字母字符串。有效的驱动器字母取决于目标架构。x86 pc 使用：a、b（软驱 1 和 2）、c（第一块硬盘）、d（第一个 CD-ROM）、n-p（通过网络适配器 1-4 进行 Etherboot），默认从硬盘启动。要仅在首次启动时应用特定的启动顺序，请通过 once 指定。
  
  只要固件/BIOS 支持，就可以通过 menu=on 启用交互式启动菜单/提示。默认是非交互式启动。
  
  可以将启动画面传递给 bios，当提供选项 splash=sp_name 且 menu=on 时，如果固件/BIOS 支持，用户可以将此作为标志显示。目前 X86 系统的 Seabios 支持此功能。限制：启动文件可以是 jpeg 文件或 24 bpp 格式（真彩色）的 bmp 文件。分辨率应支持 SVGA 模式，因此建议为 320x240、640x480、800x640。
  
  可以将超时时间传递给 bios，来宾将在启动失败时暂停 rb_timeout 毫秒，然后重新启动。如果 rb_timeout 为 '-1'，来宾将不会重新启动，qe 默认传递给 bios '-1'。目前 X86 系统的 Seabios 支持此功能。
  
  只要固件/BIOS 支持，就可以通过 strict=on 执行严格启动。这仅在通过 bootindex 选项改变启动优先级时生效。默认是非严格启动。
  
  `# 尝试先从网络启动，然后从硬盘启动`
  `qe-system-i386 -boot order=nqc`
  `# 先从 CD-ROM 启动，重启后恢复默认顺序`
  `qe-system-i386 -boot once=d`
  `# 带启动画面 5 秒启动。`
  `qe-system-i386 -boot menu=on, splash=/root/boot.bmp, splash-time=5000`
  
  注意：旧格式 'boot drives' 仍然受支持，但建议不要使用，因为它可能会在未来版本中被移除。
- `-m [size=]mem,slots=n,maxmem=size`
  - 将来宾启动 RAM 大小设置为 mem。默认为 128 MiB。可选地，可以使用后缀 "M" 或 "G" 分别表示兆字节或千兆字节的值。可选对 slots, maxmem 可用于设置可热插拔内存插槽的数量和最大内存量。注意 maxmem 必须对齐到页大小。
  
  例如，以下命令行将来宾启动 RAM 大小设置为 1GB，创建 3 个插槽以热插拔额外内存，并将来宾可达到的最大内存设置为 4GB：
  `qe-system-x86_64 -m 1G, slots=3, maxmem=4G`
  
  如果未指定 slots 和 maxmem，则不会启用内存热插拔，且来宾启动 RAM 永远不会增加。
- `-mem-path path`
  - 从 path 中临时创建的文件分配来宾 RAM。
- `-mem-prealloc`
  - 在使用 -mem-path 时预分配内存。
- `-k language`
  - 使用键盘布局语言（例如 fr 代表法语）。此选项仅在难以获取原始 pc 按键代码时需要（例如在 Mac 上、在某些 X11 服务器上或在 vnc 显示器上）。在 PC/Linux 或 PC/Windows 主机上通常不需要使用它。
  
  可用的布局包括：ar de-ch es fo fr-ca hu ja mk no pt-br sv da en-gb et fr fr-ch is lt nl pl ru th de en-us fi fr-be hr it lv nl-be pt sl tr
  
  默认为 en-us。
- `-audio-help`
  - 显示音频子系统帮助：驱动程序列表、可调参数。
- `-soundhw card1[,card2,...]` 或 `-soundhw all`
  - 启用音频和所选的声音硬件。使用 'help' 打印所有可用的声音硬件。

