
**使用生命周期规则**自动归档或删除旧资产以降低成本。

# 第 5 步：设置负载均衡器和自动伸缩

- 创建带有 EC2 配置的启动模板。
- 定义自动伸缩组：
    - i. 最小：2 个实例
    - ii. 最大：4 个实例
    - c. 伸缩策略：基于 CPU > 70%
    - d. 将应用型负载均衡器 (ALB) 挂载到组中。

监控 `/var/log/httpd/access_log` 和错误日志以进行负载测试和性能调优。

# 第 6 步：启用 CloudWatch 监控和告警

设置指标和告警：

- CPU 利用率 > 70% → 触发扩展
- CPU 利用率 < 30% → 触发缩缩

我们还可以为以下项创建告警：

- 磁盘空间 (`df -h`)
- 内存使用（使用 CloudWatch 代理）

## 安装 CloudWatch 代理以发送自定义指标：

- a. `sudo yum install amazon-cloudwatch-agent`
- b. `sudo /opt/aws/cloudwatch-agent/bin/amazon-cloudwatch-agent-ctl -c fetch-config -config /opt/aws/cloudwatch-agent/etc/config.json`

# 验证步骤

1. 通过 ALB DNS 访问应用。
2. 测试伸缩：`ApacheBench -n 1000 -c 50`。
3. 验证监控：进入 CloudWatch 观察扩展事件。

# 管理员最终注意事项

- 定期更新 Rocky Linux 和 PHP 包（`yum update`）。
- 使用 IAM 角色避免硬编码 AWS 凭据。
- 应用安全组规则以遵循最小权限原则。
- 使用自动快照备份 RDS 数据。
- 使用 CloudTrail 记录所有访问并启用 AWS Config 以进行合规性。

# 最佳实践

- 启用 AWS GuardDuty 进行威胁检测。
- 使用 Amazon Detective 深入调查安全异常。
- 定期检查 IAM 访问日志和 CloudTrail 日志。

# 实现备份策略

备份策略确保在发生系统故障、意外删除或网络攻击时维持业务连续性和数据保护。

## 最佳实践

- 定期检查 IAM 策略，识别权限过大的用户。
- 使用 IAM 组管理权限，而不是将权限分配给单个用户。
- 启用 IAM Access Analyzer 以识别未使用的权限。

# 4. 启用 HTTPS 进行安全通信

使用 HTTPS 加密传输中的数据，防止攻击者拦截信息。AWS 提供证书管理器 (ACM) 来管理 SSL/TLS 证书。

## 实施步骤

- a. 进入证书管理器并请求新证书。
- b. 使用电子邮件或 DNS 记录验证证书。
- c. 将证书附加到应用负载均衡器 (ALB) 或 CloudFront 分发中。
- d. 通过重定向 HTTP 请求到 HTTPS 来强制使用 HTTPS。

## 最佳实践

- 使用 Let us encrypt 获取免费 SSL 证书。
- 实现 HSTS（HTTP 严格传输）以强制 HTTPS。
- 定期更新轮换 SSL/TLS 证书。

# 使用 CloudTrail 和 CloudWatch 监控日志和安全事件

持续监控有助于检测并缓解安全威胁。

## 实施步骤

- a. 启用 AWS CloudTrail：
    - 进入 CloudTrail 控制台并创建轨迹。
    - 将日志存储在 Amazon S3 中进行长期留存。
- b. 为安全事件启用 CloudWatch 告警：
```bash
aws cloudwatch put-metric-alarm --alarm-name UnauthorizedLoginAttempt --metric-name FailedLogins --namespace AWS/CloudTrail --statistic Sum --threshold 5 --comparison-operator GreaterThanOrEqualToThreshold --evaluation-periods 1 --alarm-actions arn:aws:sns:us-east-1:123456789012:SecurityAlerts
```

# 实现步骤

- a. 启用 RDS 自动备份：导航至 RDS 控制台，修改实例以启用自动备份。
- b. 配置 S3 生命周期策略以进行日志保留：
```json
{
  "Rules": [
    {
      "ID": "DeleteOldLogs",
      "Status": "Enabled",
      "Prefix": "logs",
      "Expiration": { "Days": 30 }
    }
  ]
}
```
