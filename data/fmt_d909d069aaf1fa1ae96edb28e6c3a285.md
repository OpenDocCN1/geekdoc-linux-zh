
(*) 据报道，`SS2410 RAMDAC` 在 `15bpp` 模式下兼容 `AT&T20C490`。为了让服务器将其视为 `AT&T20C490`，你需要在 `XF86Config` 中提供 `Ramdac "att20c490"` 项。

`S3 801/805`, `Chrontel 8391` 时钟/显存- `JAX 8241`

- `SREA Mirage`

- `8` 和 `15/16 bpp`

`S3 928`, `AT&T 20C490 RAMDAC`- `Actix Ultra`

- `8` 和 `15/16 bpp`

注意：真实的 `AT&T20C490 RAMDAC` 应由服务器自动检测。对于其他兼容设备，你需要在 `XF86Config` 中提供 `Ramdac "att20c490"` 项。`8391` 兼容 `AT&T20C490 RAMDAC`。真实的 `T20490` 或 `20C41 RAMDAC` 支持 `dac_8_bit`。某些克隆版本（如 `Winbond 82C490`）不支持。

```
ClockChip "8391"
RamD "8391"
Option "dac_8_bit"
```

# 第140页 第3章：安装 Linux 和网络组件

`8, 15/16` 和 `24(32) bpp`

`S3 864`, `AT&T20C498` 或 `ST1700 RAMDAC`, `ICD2061A` 或 `ICS9161 Clockchip`

- `Elsa Winner1000PRO VLB` 所有- `Elsa Winner1000PRO PCI`

- `MIRO 205D (BIOS 2.xx)` 所有- `Actix GraphicsEngine 64 VLB/2MB`

- `8, 15/16` 和 `24(32) bpp`

### 时钟芯片 "icd2061a"

`S3 864`, `20C498` 或 `21C498 RAMDAC`, `ICS2595 Clockchip`

时钟的支持有时仍然不稳定。在某些机器上，可能会看到启动后 `XF86_S3` 模式或从 `VT` 切回后的第一个模式出现问题；通过 `CTRL+ALT+'KP+''` 切换到下一个模式再切回来似乎可以解决这个问题。

隔行模式（Interlaced modes）无法正常工作。

`BIOS 4.xx` 的 `Mirage P64` 使用 `S3 DAC`。

### 时钟芯片 "ics2595"

`S3 864`, `S3 86C716 SDAC RAMDAC` 和 `Clockchip`

- `Elsa Winner1000PRO`

- `MIRO 205D (BIOS 3.xx)`

- `MirageP64 2MB DRAM (BIOS 4.xx)`

- `Diamond Stealth 64 DRAM`

- `8, 15/16` 和 `24 bpp`

`S3 864`, `ICS5342 RAMDAC` 和 `Clockchip`

- `Diamond Stealth 64 DRAM`（仅部分显卡）

- `8, 15/16` 和 `24 bpp`

### 时钟芯片 "ics5342"

`Ramdac "ics5342"`

# 第141页 第3章：安装 Linux 和网络组件

`S3 864`, `AT&T21C498-13 RAMDAC`, `ICD2061A Clockchip`

- `#9 GXE4 - PCI`

`8, 15/16, 24(32) bpp`

`ClockChip "icd2061a"`

选项 `"number_nine"`

`S3 964`, `AT&T 20C505 RAMDAC`, `ICD2061A Clockchip`

- `Miro Crystal 20SV`

`8, 15/16, 24(32) bpp`

`ClockChip "icd2061a"`

`Ramdac "att20c505*"`

`S3 964`, `Bt485 RAMDAC`, `ICD2061A Clockchip`

- `Diamond Stealth 64`

`8, 15/16, 24(32) bpp`

`ClockChip "icd2061a"`

`S3 964`, `Bt9485` 或 `AT&T 20C505 RAMDAC`, `ICS9161a Clockchip`

- `SPEA Mercury 64`

`8, 15/16, 24(32) bpp`

`ClockChip "ics9161a"`

选项 `"SPEA_Mercury*"`

`S3 964`, `Ti3020 RAMDAC`, `ICD2061A Clockchip`

- `Elsa Winner2000PRO PCI`

`8, 15/16, 24(32) bpp`

`ClockChip "icd2061a"`

`S3 964`, `Ti3025 RAMDAC`, `Ti3025 Clockchip`

- `Miro Crystal 40SV`

- `#9 GXE64 Pro VLB`

- `#9 GXE64 Pro PCI`

`8 bpp, 15, 16` 和 `24(32) bpp`

# 第142页 第3章：安装 Linux 和网络组件

`GXE64 Pro` 存在一些已知问题，包括在 `15/16/24 bpp` 下出现某些图像偏移/包裹问题。

我们发现 `#9` 不再支持 `1600x1200` 分辨率下的 `GXE64 Pro`。不过他们有一块新的（且更贵的）板卡称为 `GXE64Pro-1600`，它使用了 `220MHz` 的 `RAMDAC`，而不是其他板卡上使用的 `13MHz` 部。

### S3 764 (Trio64)

- `SPEA Mirage P64 (BIOS 5.xx)`

- `Diamond Stealth 64 DRAM`

- `#9 GXE64 Trio64`

- `15/16/24 bpp`

注意：`Trio64` 内置了 `RAMDAC` 和时钟芯片，因此服务器应兼容所有 `Trio64` 显卡，无需在 `XF86Config` 文件中指定 `RAMDAC` 或时钟芯片。

### S3 732 (Trio32)

- `Diamond Stealth 64 DRAM SE`

- `15/16/24 bpp`

注意：`Trio32` 内置了 `RAMDAC` 和时钟芯片，因此服务器应兼容所有 `Trio32` 显卡，无需在 `XF86Config` 文件中指定 `RAMDAC` 或时钟芯片。

### S3 868, S3 86C716 SDAC RAMDAC 和 Clockchip

- `ELSA Winner 1000`

- `15/16/24 bpp`

`S3 968`, `Ti3026 RAMDAC`, `Ti3026 Clockchip`

- `Elsa Winner 2000PRO/X`

- `Diamond Stealth 64 VRAM`

- `15/16/24 bpp`

`S3 964`, `IBM RGB 514/524/525/528 RAMDAC & Clockchip`

- `Hercules Terminator 64`

# 第143页 第3章：安装 Linux 和网络组件

`S3 968`, `IBM RGB 514/524/525/528 RAMDAC & Clockchip`

- `Genoa VideoBlitz`

`S3 968`, `IBM RGB 514/524/525/528 RAMDAC & Clockchip`

- `Hercules Pro 64`

此显卡可能需要以下行：

`Invert_VCLK 0`

在每个显示子部分。

- `STB Velocity 64`

`s3RefClk 24 DACspeed 220`

- `Number Nine 771`

`s3RefClk 16 DACspeed 220`

`15/16/24 bpp`

### 16bpp 和 32bpp

在 `80+ AT&T490` 显卡（如 `Fahrenheit 128+`）上仅支持 `15` 和 `16bpp`。该类型的显卡不支持 `32bpp`（在 Windows 下有一个 `24 bit` 模式，但不是真正的 `32bpp`）。

`AT&T20C490-11`

`9339ES`

`98698`

# 第3章：安装 Linux 和网络组件

这是速率为 `110 MHz` 的 `AT&T 20C490`。这意味着要在 `XF86Config` 文件中添加 `DacSpeed 110` 行。注意，某些 `RAMDAC` 具有不同限制的模式。制造商总是以较高的限制来标记芯片，因此应小心。`S3` 服务器知道如何处理大多数 `RAMDAC` 的模式并提供正确的 `DacSpeed`。

标记为 `-80` 或 `-8` 的芯片应在设备部分使用 `DacSpeed 80`：

`S3 86C716-ME SDAC ==> DacSpeed 110`

`SC1525-8 ==> DacSpeed 80`

`AT&T20C490-80 ==> DacSpeed 80`

`IBM 8190429 ==> DacSpeed 170`

`IBM 03H5428 ==> DacSpeed 170`

`IBM 03H6447 ==> Speed 170`

`IBM 03H6448 ==> DacSpeed 220`

`IBM 03H5319 ==> DacSpeed 220`

`IBM 63G9902 ==> DacSpeed 250`

`IBM 37RGB54CF17 ==> DacSpeed 170`

`IBM 37RGB54CF22 ==> DacSpeed 220`
