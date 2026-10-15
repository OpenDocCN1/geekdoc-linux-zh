

## Part I: 为 Firefox 浏览器创建配置文件

执行以下操作：

- 1. 启动 Yast，输入 root 密码（novell）。
- 2. 选择 Novell AppArmor > Add Profile Wizard。
- 3. 在提示 Application to Profile 时，输入 firefox。
- 4. 按 Alt+F2 启动 Firefox，输入 firefox 并选择 Run。浏览一些网页。再次关闭 Firefox。
- 5. 在 YaST AppArmor Profile Wizard 对话框中，选择 Scan system log for AppArmor events。
- 6. 现在你创建配置文件并需要回答几个问题。请注意 Firefox 应用程序相当复杂，会访问系统上的多个可执行文件和文件。
- a. 对于 /bin/basename 和其他被执行的程序，选择 Inherit。
- b. 对于文件和目录，选择合适的选项，例如 #include、文件名、目录或带占位符的路径，并选择 Allow。
- 7. 当你返回到 AppArmor Profile Wizard 对话框时，选择 Finish。
- 8. 通过使用 cat 查看 /sys/kernel/security/apparmor/profiles，确保 Firefox 配置文件处于 enforce 模式。必须存在条目 /usr/lib/firefox/firefox.sh (enforce)。如果没有，执行 enforce firefox。

## Part II: 修改 Firefox 的配置文件以允许读取本地文件系统

执行以下操作：

- 1. 打开一个终端窗口并 su - 切换到 root（密码 novell）。
- 2. 输入 tail -f /var/log/audit/audit.log。
- 3. 按 Alt+F2 启动 Firefox，输入 firefox 并选择 Run。尝试查看文件 /usr/share/doc/packages/apparmor-docs/apparmor.7.html。（你应该无法做到。）
- 4. 在终端窗口中查看日志文件。你应该会看到一条 reject 消息。
- 5. 通过按 Ctrl+c 停止查看日志文件。
- 6. 在终端窗口中，输入 complain firefox。
- 7. 在 Firefox 中，再次尝试访问 /usr/share/doc/packages/apparmor-docs/apparmor.7.html。你现在应该能够访问该文件。
- 8. 启动 Yast，输入 root 密码（novell）。
- 9. 选择 Novell AppArmor > Update Profile Wizard。
- 10. 你会看到与 Part I 相同的界面，可以选择 Allow、Inherit、Deny 等。确保你正在更新 Firefox 配置文件，而不是其他配置文件。
  最终你应该会看到路径 /usr/share/doc/packages/apparmor-docs/apparmor.7.html 的条目。通过三次选择 Glob 按钮，可以创建一个建议 /usr/share/doc/**。通过选择 Allow 允许它。
- 11. 当日志文件中的所有条目都已处理完毕时，选择 Finish。
- 12. 通过在终端窗口中输入 enforce firefox 将 Firefox 配置文件重新置于 enforce 模式。

10. 再次启动 Firefox 并选择在步骤 4 中给出的 URL 可用的另一个 Java 演示。这现在应该可以工作，尽管配置文件已再次处于 enforce 模式。

## Part IV: 将你创建的配置文件与 SLES 10 中的配置文件进行比较

执行以下操作：

- 1. 打开一个控制台窗口并使用 cat 查看刚创建的配置文件 /etc/apparmor.d/usr.lib.firefox.firefox.sh。
- 2. 打开另一个控制台窗口并使用 cat 查看配置文件 /etc/apparmor/profiles/extras/usr.lib.firefox.firefox*。
- 3. 比较这些文件。注意任何差异并决定它们是否比你创建的配置文件更严格。

（练习结束）

## Objective 3 Control AppArmor

可以使用脚本 **/etc/init.d/boot.apparmor** 或指向该脚本的链接 **/sbin/rcapparmor** 来控制 AppArmor。该脚本接受通常的参数 start、stop 等，但由于 AppArmor 不是守护进程，其意义略有不同。

要控制 AppArmor，你需要知道如何

- Start and Stop AppArmor
- View AppArmor's Status
- Reload Profiles

### Start and Stop AppArmor

要限制应用程序，AppArmor 必须在应用程序启动之前处于活动状态。因此，AppArmor 通常在启动过程的早期激活。

如果你不再希望 AppArmor 限制你的应用程序，使用 **rcapparmor stop**。这会卸载配置文件，但 AppArmor 内核模块 apparmor 和 aamatch_pcre 仍保持加载。**rcapparmor kill** 也会卸载内核模块。在这两种情况下，应用程序都不会再被限制。

**rcapparmor start** 激活 AppArmor。但是，只有在 AppArmor 激活后启动的应用程序才会被限制。即使例如存在 Squid 的配置文件，如果你在启动 AppArmor 之前就已运行 Squid，Squid 也不会被限制。要将 Squid 纳入 AppArmor 的保护，你需要在激活 AppArmor 后重新启动 Squid。

