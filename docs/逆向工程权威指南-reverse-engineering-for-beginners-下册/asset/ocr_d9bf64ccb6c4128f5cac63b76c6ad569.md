# # 附录B ARM

# ## B.1 术语

初代ARM处理器就是32位CPU。所以它的word型数据都是32位数据。这方面它和x86有所不同。

+   - byte 8位数据。声明byte型数组和变量的指令是DB。
- halfword 16位数据。声明halfword型数组和变量的指令是DCW。
- word 32位数据。声明word型数组和变量的指令是DCD。
- doubleword 64位数据。
- quadword 128位数据。

# ## B.2 版本差异

+   - ARMv4: 开始支持Thumb模式的指令。
- ARMv6: 用于第一代iPhone、iPhone 3G（这些设备的处理器采用了Samsung 32位RISC ARM 1176IZ (F) -S，支持Thumb-2指令）。
- ARMv7: 实现了Thumb-2指令（2003）。用于iPhone 3GS、iPad 1（ARM Cortex-A8）、iPad 2（Cortex-A9）和iPad 3。