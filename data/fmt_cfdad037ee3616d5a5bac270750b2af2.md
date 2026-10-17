
1. 从磁盘加载 `z/VM` 操作系统。这包括系统 `CP` 核心。

2. `CP` 读取 `SYSTEM CONFIG` 文件，以识别配置参数并实施这些参数。

3. 操作系统将 `CP` 所拥有的卷联机，例如用于分页、排队和 `t-disk` 的卷。

4. 根据启动方式（参见 5.2.2，第 234 页的“Warm start, force start, cold start, and clean start”），`z/VM` 在上次关机期间读取保存在检查点和热启动数据文件²中的系统属性信息并将其恢复。

5. 系统提示设置时间-日期（`TOD`）。

6. 用户目录，连同用户的定义，一并联机。

7. 现有的 `spool` 文件可供使用。

8. 所有已连接的 `I/O` 联机并可供使用。

9. `SYSTEM CONFIG` 中定义的用户卷可供使用。

10. `OPERATOR` 用户已登录。

11. `OPERATOR` 虚拟机通过登录 `erep`、`diskacct` 和 `opersymp` 用户来启动日志/记账/症状服务。

12. `OPERATOR` 用户 ID 自动登录 `AUTOLOG1`。

13. `AUTOLOG1` 根据其 `PROFILE EXEC` 启动其被指示启动的任何其他虚拟机。

14. 服务机器在初始化状态下向 `OPERATOR` 发送消息。

## Example 5-1 z/VM IPL process
