
## Kubernetes 插件

### 模块
- `k8s_info` - 描述 Kubernetes (K8s) 资源
- `k8s_json_patch` - 向操作对象应用 JSON patch
- `k8s_log_module` - 从 kubernetes 资源获取日志
- `k8s_deployment` - 管理 K8s Deployments 和 DaemonSets
- `k8s_scale_module` - 为 Deployment, ReplicaSet 或 job 设置新大小
- `k8s_service` - 管理 Kubernetes 中的 Services

### 连接插件
- `kubectl connection` - 在 pods 中执行任务

### 过滤器插件
- `k8s_config_resource_name` - 为给定类型的 ConfigMap, Secret 生成资源名称

### 清单插件
- `k8s inventory` - Kubernetes (K8s) 清单源

### 查找插件
- `k8s lookup` - 查询 K8s API
- `kustomize` - 使用 'customization.yaml' 文件构建一组资源

### VMware Rest

版本 2.3.1

https://docs.ansible.com/ansible/latest/collections/vmware/vsphere/index.html#plugins-in-vmware-rest

- `vware_access_console_module` - 设置受控制的基础 CLI (TTY1) 的启用状态
- `vware_access_console_info` - 获取受控制的基础 CLI (TTY1) 的启用状态
- `vware_access_dcu_module` - 设置直接控制接口 (DCU TTY2) 的启用状态
- `vware_access_dcu_info` - 获取直接控制接口 (DCU TTY2) 的启用状态
- `vware_access_shell_module` - 设置 SSH 的启用状态，以便从受控制 CLI 访问 B
- `vware_access_shell_info` - 获取受控制 CLI 内部 SSH 的启用状态
- `vware_access_ssh_module` - 设置 SSH 控制 CLI 的启用状态
- `vware_access_ssh_info` - 获取 SSH 控制 CLI 的启用状态
- `vware_health_module` - 获取已批准服务的状态
- `vware_health_info` - 获取数据库状态
- `vware_health_database_module` - 获取数据库状态
- `vware_load_module` - 获取加载
- `vware_inventory_module` - 获取清单信息
- `vware_softwarepackages_info` - 获取 vSphere 中的可用软件信息
- `vware_storage_info` - 获取存储信息
- `vware_system_module` - 获取系统的整体健康状况
- `vware_infrastructure_config_plugins` - 列出所有注册的插件
- `vware_locationacl_global_module` - 设置全局策略
- `vware_locationacl_global_info` - 获取全局策略
- `vware_user_module` - 获取用户账户
- `vware_monitoring_module` - 获取监控项
- `vware_monitoring_info` - 获取监控数据
- `appliance_info_module` - 获取 NTP 服务器
- `appliance_service_module` - 获取 NTP 配置状态
- `appliance_service_module` - 返回服务的状态
- `appliance_shutdown_module` - 返回关机操作
- `appliance_info_module` - 获取待关机操作的详情
- `appliance_global_fips_module` - 为设备启用/禁用 FIPS 模式
- `appliance_global_fips_module` - 获取设备当前的 FIPS 设置
- `appliance_system_storage_module` - 将分区调整调整为磁盘大小的 100%
- `appliance_system_storage_module` - 获取分区映射的详情
- `appliance_time_module` - 获取时区
- `appliance_time_module` - 设置时区
- `appliance_time_module` - 获取时区。获取时区。
- `appliance_version_module` - 获取版本
- `appliance_version_module` - 获取时间同步模式
- `appliance_timesync_module` - 获取时间同步
- `appliance_info_module` - 获取设备的当前状态
- `appliance_vm_service_module` - 获取由 VM 管理的服务详情
- `appliance_vm_service_module` - 返回服务的状态
- `content_info_module` - 获取配置
- `content_info_module` - 根据标识符检索配置值
- `content_locallibrary_module` - 创建新的本地
- `content_locallibrary_module` - 获取本地库
- `content_subscribed_module` - 创建新的订阅
- `content_subscribed_module` - 返回订阅库
- `content_guest_module` - 获取指定的库
- `vcenter_datastore_module` - 在 vCenter 清单中创建新的数据存储
- `vcenter_datastore_module` - 获取对应于 (`@param.name_datastore`)的数据存储
- `vcenter_datastore_module` - 根据 (`@param.name_datastore`) 获取关于数据存储的信息
- `vcenter_folder_module` - 向 vCenter 清单中添加新文件夹
- `vcenter_folder_module` - 允许 vCenter 中最多 2500 个（取决于权限检查）匹配 (`@link FolderFilterSpec`) 的主机
- `vcenter_network_module` - 添加新网络
- 获取 vCenter 中多最多 1000 个（取决于权限检查）匹配 (`@link FilterSpec`) 的可见网络信息
- `vcenter_ov_library_module` - 从虚拟机或虚拟设备创建库项
- `vcenter_resourcepool_module` - 根据 (`@param.name_resourcePool`) 获取资源池
- `vcenter_storage_module` - 获取 v 中可用的（取决于权限检查）可见存储策略信息
- `vcenter_vm_module` - 创建虚拟机
- `vcenter_vm_customization_module` - 在客机操作系统中创建客户
- `vcenter_vm_filesystem_module` - 获取操作系统中文件的信息
- `vcenter_vm_guest_module` - 返回客机操作系统中客户配置的详情
- `vcenter_vm_networking_module` - 获取客机操作系统网络接口的信息
- `vcenter_vm_networkrouting_module` - 获取客机操作系统网络路由的信息
- `vcenter_vm_operations_module` - 获取客机操作的信息
- `vcenter_vm_power_module` - 向客机操作系统发送请求以执行软关机、（挂起）或软重启
- `vcenter_vm_hardware_module` - 获取虚拟机的硬件
- `vcenter_hardware_adapter_module` - 向虚拟机添加 SATA 设备
- `vcenter_hardware_adapter_module` - 获取关于 SATA 适配器设备的信息
- `vcenter_hardware_scsi_module` - 向虚拟机添加 SCSI 设备
- `vcenter_hardware_scsi_module` - 获取关于 SCSI 适配器设备的信息
- `vcenter_hardware_settings_module` - 获取虚拟机的启动设置
- `vcenter_hardware_boot_module` - 设置将用于启动虚拟机的设备
- `vcenter_hardware_boot_module` - 获取虚拟机的启动设置
- `vcenter_hardware_cdrom_module` - 向虚拟机添加 CD-ROM 设备
- `vcenter_hardware_cdrom_module` - 获取关于 CD-ROM 设备的信息
- `vcenter_hardware_cpu_module` - 更新虚拟机的 CPU 设置
