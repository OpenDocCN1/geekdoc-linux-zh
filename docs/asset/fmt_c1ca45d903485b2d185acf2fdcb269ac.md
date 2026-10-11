
# 图形类库 181

- 使用 `SDL` 打印 "Hello, world!" 182

- 初始化库 183

- 初始化帧缓冲 183

- 创建表面 (`Surface`) 184

- 显示表面 184

处理事件 185

图形工具包 185

- 使用 `STBmenu` 构建简单 UI 187

- 使用 `STBmenu` 打印 "Hello, world!" 190

`Laddie` 帧缓冲 UI 193

总结 196

# 13 实战： SNMP 简介 223

术语快速速览 224

软件 225

安装 `SNMP` 225

下载与安装 226

检查安装 226

配置代理 227

启动代理 227

探索 `SNMP` 228

可读 `MIB` 文件 229

网络打印机 231

`snmtrapd` 命令 231

`MIB-2`: TCP 连接表 232

`MIB-2`: UDP 表 233

`MIB-2` 内容 233

使用 `SNMP` 设置值 235

设置 `sysContact` 235

设置 `sysName` 237

`SNMP` 陷阱 238

使用 `snmtrapd` 接收陷阱 238

携带数据的陷阱：`linkUp` 和 `linkDown` 240

总结 242

# 14 设计 SNMP MIB 243

我们的目标 244

企业编号 245

`MIB` 文件 246

`LADDIE-GROUP-SMI` 246

创建 `LADIE-MIB` 249

模块定义 251

版本与区域数量 253

报警表 255

陷阱 257

验证你的 `MIB` 259

总结 260

# 15 实现你的 SNMP MIB 261

- `Net-SNMP` 代理 262

- `MIB` 骨架：`mib2c` 265

- 头文件：`ladProject.h` 267

- 代码文件：`ladProject.c` 267

- 包含文件 268

- 基础 `OID` 268

- `MIB` 对象定义 268

- `RTA` 访问例程 271

- 初始化程序 274

- 标量 (`Scalars`) 275
