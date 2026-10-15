
# 配额说明

配额对于确保开发者之间的公平资源共享也至关重要。否则，一个决定将 PC 备份到服务器上主目录并完全填满分区的开发者可能会阻止其他用户写入数据。

除了这些考虑外，从管理的角度来看，实施配额是最优的：它迫使用户合理规划自己的存储，以确保材料不被浪费。

## 设置用户额配额

为了设置用户额配额，可以执行以下步骤：

1. 在 `/etc/fstab` 中启用 ``。
2. 在 `/staff` 目录下添加 `quota` 选项。
3. 在 `/staff` 目录下运行 `edquota`。
4. 在 `/staff` 目录下运行 `quota -v`。
5. 在 `/staff` 目录下运行 `quota -u`。
6. 在 `/staff` 目录下运行 `quota -g`。
7. 在 `/staff` 目录下运行 `quota -a`。
8. 在 `/staff` 目录下运行 `quota -p`。
9. 在 `/staff` 目录下运行 `quota -t`。
10. 在 `/staff` 目录下运行 `quota -m`。
11. 在 `/staff` 目录下运行 `quota -q`。
12. 在 `/staff` 目录下运行 `quota -i`。
13. 在 `/staff` 目录下运行 `quota -s`。
14. 在 `/staff` 目录下运行 `quota -c`。
15. 在 `/staff` 目录下运行 `quota -w`。
16. 在 `/staff` 目录下运行 `quota -x`。
