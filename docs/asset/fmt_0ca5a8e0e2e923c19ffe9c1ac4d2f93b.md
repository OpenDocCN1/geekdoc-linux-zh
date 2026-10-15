
# Linux Components

## Settings

### Auto Settings

### DTG Settings

### MPMC Configuration

### SBL Configuration

### IBN Trusted Firmware Configuration

### FPGA Manager

### U-boot Configuration

### Image Packaging Configuration

### Firmware Version Configuration

`(*)`

`<Select>` `< Exit >` `< Help >` `< Save >`

```
- 3) 选择 SD/DIO Settings
```

`system Settings Settings`

`Arrow keys navigate the menu. <enter> selects submenu (or empty ubmenu...). Highlighted letters are hotkeys. Press <Y>`

`Includes, <n> excludes, <*> modular features. Press <Esc><Esc> to exit, <?> for Help, < /> for Search`

- Subsystem AUTO Hardware Settings

`System Processor (psu_cortex53_0) ---`

`Memory Settings ---`

`Serial Settings --nEthernet Settings ---`

`Flash Settings ---`

`SD/DIO Settings ---`

`RTC Settings ---`

`[*] Advanced boot images storage settings ---`

`<Select>` `< Exit >` `< Help >` `< Save >`

![](img/6f792577a28af84c82be0eef5006ef77_89_0.png) 4) 选择对应 eMMC 的 SDIO（如果不确定，请尝试）

![](img/6f792577a28af84c82be0eef5006ef77_90_0.png)- 5) 保存并退出配置界面，重新编译系统。

- 6) 将编译得到的图中所示的三个文件拷贝到开发板 NFS 挂载的文件夹中。

- 7) 将 FPGA 开发板系统中的这三个文件拷贝到 eMMC 挂载的目录。

- 8) 拷贝完成后，使用 `umount` 命令卸载 eMMC。

- 9) 断开开发板电源，将拨开关拨到 eMMC 启动状态，然后重新上电。
