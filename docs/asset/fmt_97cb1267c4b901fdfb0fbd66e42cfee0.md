
# vCenter 硬件模块

`vcenter_hardware_cpu_module` - 获取虚拟机的 CPU 设置

`vcenter_hardware_disk_module` - 向虚拟机添加磁盘

`vcenter_hardware_disk_module` - 获取关于磁盘的信息

`vcenter_hardware_ethernet_module` - 向虚拟机添加以太网适配器

`vcenter_hardware_ethernet_module` - 获取关于以太网适配器的信息

`vcenter_hardware_floppy_module` - 向虚拟机添加软盘

`vcenter_hardware_floppy_module` - 获取关于软盘的信息

`vcenter_memory_module` - 获取虚拟机的内存设置

`vcenter_memory_module` - 获取虚拟机的内存设置

`vcenter_parallel_module` - 向虚拟机添加并行端口

`vcenter_parallel_module` - 获取关于并行端口的信息

`vcenter_serial_module` - 向虚拟机添加串口端口

`vcenter_serial_module` - 获取关于串口端口的信息

`vcenter_library_module` - 获取客机上的库信息

`vcenter_power_module` - 获取虚拟机的电源状态

`vcenter_storage_module` - 更新虚拟机及其关联磁盘的存储策略

`vcenter_storage_compliance_module` - 复制检查后的存储策略

`vcenter_storage_compliance_module` - 获取虚拟机的存储合规性

`vcenter_storage_policy_module` - 获取关于虚拟机目录的存储策略

## vcenter_tools_7.0

## Amazon AWS

- `scaling-collections` 创建或删除自动扩展组 (ASGs)

- `autoscaling_group_info` - 获取自动扩展组 (ASGs)

- `autoscaling_group_info` - 获取自动扩展组 (ASGs)

- `aws_caller_info` - 获取调用 AWS 的用户信息

- `ec2_instance_info` - 获取 EC2 实例的信息

- `ec2_backup_plan` - 获取备份任务的信息

- `ec2_backup_selection` - 创建备份选择

- `ec2_backup_selection` - 获取备份选择的信息

- `ec2_tag_manage` - 管理 EC2 资源的标签

- `ec2_tag_info` - 列出 EC2 资源的标签

- `ec2_vault_manage` - 管理 EC2 库

- `ec2_vault_info` - 描述 EC2 库

- `cloudformation_stack` - 创建或删除 CloudFormation 栈

- `cloudformation_info` - 获取 AWS CloudFormation 信息

- `cloudtrail_manage` - 创建或删除 CloudTrail

- `cloudtrail_info` - 获取 CloudTrail 的信息

- `cloudwatch_metric_alarm` - 创建或删除 CloudWatch 指标警报

- `cloudwatch_metric_info` - 获取特定指标的警报信息

- `cloudwatch_event_rule` - 管理 CloudWatch 事件规则和目标

- `cloudwatch_logs_manage` - 创建或删除 CloudWatch 日志组

- `cloudwatch_logs_info` - 获取 CloudWatch 日志组的信息

- `cloudwatch_logs_metric_filter` - 管理 CloudWatch 日志指标过滤器

- `cloudwatch_logs_metric_filter_info` - 获取日志指标过滤器信息

- `ec2_ami_manage` - 创建并删除 AMI

- `ec2_ami_info` - 获取 EC2 AMI 信息

- `ec2_eip_manage` - 创建并删除 EIP

- `ec2_eip_info` - 列出 EIP 地址

- `ec2_eni_manage` - 创建并将弹性网络接口 (ENI) 附加到实例

- `ec2_eni_info` - 获取 AWS 中的 ENI 接口信息

- `ec2_instance_manage` - 创建并管理 EC2 实例

- `ec2_instance_info` - 获取 EC2 实例信息

- `ec2_key_manage` - 创建或删除 EC2 密钥对

- `ec2_key_info` - 获取 AWS 中的 EC2 密钥对信息

- `ec2_metadata_facts` - 收集 EC2 远程主机的事（实例元数据）

- `ec2_security_group_manage` - 管理 EC2 安全组

- `ec2_security_group_info` - 获取 EC2 安全组的信息

- `ec2_snapshot_manage` - 从现有卷创建快照

- `ec2_snapshot_info` - 获取 AWS 中 EC2 卷快照的信息

- `ec2_spot_manage` - 请求、停止、重启或取消竞价实例

- `ec2_spot_info` - 获取 EC2 竞价实例的信息

- `ec2_tag_manage` - 在 EC2 资源上创建和删除标签

- `ec2_tag_info` - 列出 EC2 资源的标签

- `ec2_volume_manage` - 通过 ID 和名称创建、删除或调整卷

- `ec2_volume_info` - 获取 EC2 卷的信息

- `ec2_vpc_option` - 创建并确保给定 VPC 的 DHCP 选项符合请求

- `ec2_vpc_option_info` - 获取 AWS 中的 VPC 选项

- `ec2_endpoint_manage` - 创建或删除 VPC 端点

- `ec2_endpoint_info` - 使用 AWS 获取 VPC 端点信息

- `ec2_endpoint_service_manage` - 管理 AWS 端点服务详情

- `ec2_endpoint_service_info` - 获取 AWS 端点服务信息

- `ec2_ig_manage` - 在 AWS 中创建或删除互联网网关

- `ec2_ig_info` - 获取 AWS 中互联网网关的信息

- `ec2_nat_gateway_manage` - 使用 AWS 方法创建或删除 NAT 网关

- `ec2_nat_gateway_info` - 使用 AWS 方法获取 NAT 网关信息

- `iam_user` - AWS IAM 用户

- `iam_policy` - 在 AWS 中创建 IAM 策略

- `kms_key_module` - 执行 KMS 密钥管理任务

- `kms_info_module` - 收集有关 AWS KMS 密钥的信息

- `lambda_module` - 创建 AWS Lambda 函数

- `lambda_event_module` - 创建、更新或删除 AWS Lambda 事件映射

- `lambda_function_module` - 管理 AWS Lambda 函数

- `lambda_info_module` - 收集 AWS Lambda 函数详情

- `s3_bucket_module` - 创建、更新或删除 AWS S3 存储桶实例

- `s3_layer_module` - 列出 S3 层或对象层版本

- `s3_policy_module` - 创建、更新或删除 AWS S3 策略语句

- `rds_cluster_module` - 获取 RDS 集群信息

- `rds_instance_module` - 收集更多 RDS 实例信息

- `rds_instance_module` - 管理 RDS 实例

- `rds_snapshot_module` - 收集一个或多个 RDS 快照

- `option_group_module` - 管理 RDS 选项组的连接、修改和删除

- `rds_param_module` - 管理 RDS 参数组

- `rds_storage_module` - 收集一个或多个 RDS 存储信息

- `rds_subnet_module` - 在 Amazon Route53 DNS 服务中添加或删除子网

- `route53_health_module` - 管理 Amazon Route53 服务中的健康检查

- `route53_info_module` - 使用 AWS 方法检索 Route53 详情

- `s3_bucket_module` - 管理 AWS、Glacier、Wake、False S3 和 StorageGRID 中的 S3 存储桶

- `s3_object_module` - 管理 S3 中的对象

- `s3_object_module` - 收集 S3 中对象的信息

## Callback
