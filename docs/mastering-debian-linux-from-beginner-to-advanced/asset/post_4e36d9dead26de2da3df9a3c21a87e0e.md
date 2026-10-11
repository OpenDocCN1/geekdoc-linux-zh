
# # Other Useful Monitoring Tools

To run iostat:

```
iostat
```

Key features of iostat:

- CPU statistics: Displays CPU utilization report.
- Device utilization: Shows I/O statistics for each device.
- Extended options: Provides detailed reports with additional flags.

Useful iostat options:

- `-c`: Display CPU utilization report only.
- `-d`: Display device utilization report only.
- `-x`: Display extended statistics.
- `-p`: Display statistics for block devices and all their partitions.

Example usage:

```
iostat -x 5 3
```

This command will display extended statistics every 5 seconds for 3 iterations.

### Other Monitoring Tools

- **vmstat**: Reports information about processes, memory, paging, block I/O, traps, and CPU activity.
  ```
  vmstat 5 3
  ```
- **free**: Displays the amount of free and used memory in the system.
  ```
  free -h
  ```
- **df**: Reports file system disk space usage.
  ```
  df -h
  ```
- **du**: Estimates file and directory space usage.
  ```
  du -sh /path/to/directory
  ```
- **sar**: Collects, reports, and saves system activity information.
  ```
  sudo apt install sysstat
  sar -u 5 3
  ```

# Diagnosing Boot and Kernel Issues

Boot and kernel issues can be particularly challenging to diagnose and resolve. Here are some strategies and tools to help you troubleshoot these problems.

## Understanding the Boot Process

1. **BIOS/UEFI**: Performs hardware initialization and loads the bootloader.
2. **Bootloader (e.g., GRUB)**: Loads the kernel and initial ramdisk (initrd).
3. **Kernel**: Initializes hardware and mounts the root filesystem.
4. **init system (e.g., systemd)**: Starts system services and brings the system to a usable state.

## Common Boot Issues and Solutions

1. **GRUB rescue prompt**:
   - Issue: GRUB configuration is incorrect or corrupted.
   - Solution: Boot from a live USB, chroot into the system, and reinstall GRUB.
2. **Kernel panic**:
   - Issue: The kernel encounters a fatal error and cannot continue.
   - Solution: Boot into an older kernel version, check hardware compatibility, or update the kernel.
3. **Failed to start service**:
   - Issue: A critical system service fails to start during boot.
   - Solution: Check service logs, repair configuration files, or disable the problematic service temporarily.

## Tools for Diagnosing Boot Issues

1. **journalctl**: Access system logs to identify boot-related errors.
   ```
   journalctl -b
   ```
2. **dmesg**: Display kernel ring buffer messages.
   ```
   dmesg | less
   ```
3. **systemd-analyze**: Analyze boot time and identify slow-starting services.
   ```
   systemd-analyze blame
   ```
4. **Boot parameters**: Add kernel parameters to troubleshoot specific issues.
   - Edit GRUB menu entry and add parameters like `nomodeset`, `acpi=off`, or `single` for different troubleshooting scenarios.

### Kernel-related Troubleshooting

1. **Checking kernel version**:
   ```
   uname -r
   ```
2. **Listing installed kernels**:
   ```
   dpkg --list | grep linux-image
   ```
3. **Removing old kernels**:
   ```
   sudo apt autoremove
   ```
4. **Updating the kernel**:
   ```
   sudo apt update
   sudo apt upgrade
   ```
5. **Compiling a custom kernel**: For advanced users who need specific features or optimizations.

# Log Management in Debian

Effective log management is crucial for troubleshooting, security monitoring, and system maintenance. Debian uses various logging mechanisms to record system events, application activities, and user actions.

## Common Log Locations

1. **/var/log**: The main directory for system logs.
2. **/var/log/syslog**: General system messages and events.
3. **/var/log/auth.log**: Authentication and authorization-related logs.
4. **/var/log/kern.log**: Kernel messages.
5. **/var/log/apache2/**: Apache web server logs (if installed).
6. **/var/log/mysql/**: MySQL database logs (if installed).

## Log Rotation

Log rotation is the process of archiving and compressing old log files to prevent them from consuming too much disk space. Debian uses the `logrotate` utility to manage log rotation.

Key features of logrotate:

1. Automatically rotates, compresses, and removes log files.
2. Configurable rotation frequency (daily, weekly, monthly).
3. Customizable retention periods for archived logs.

To view logrotate configuration:

```
cat /etc/logrotate.conf
```

To manually run logrotate:

```
sudo logrotate -f /etc/logrotate.conf
```

## Log Analysis Tools

1. **grep**: Search for specific patterns in log files.
   ```
   grep "error" /var/log/syslog
   ```
2. **tail**: Display the last few lines of a log file in real-time.
   ```
   tail -f /var/log/syslog
   ```
3. **awk**: Process and analyze log data.
   ```
   awk '/error/ {print $0}' /var/log/syslog
   ```
4. **sed**: Edit log files or transform log data.
   ```
   sed 's/error/ERROR/g' /var/log/syslog
   ```
5. **logwatch**: Analyzes log files and generates reports.
   ```
   sudo apt install logwatch
   sudo logwatch --output stdout --format text --range today
   ```

# Remote Logging

For centralized log management, you can configure your Debian system to send logs to a remote syslog server.

1. Edit the rsyslog configuration file:
   ```
   sudo nano /etc/rsyslog.conf
   ```
2. Add the following line to send logs to a remote server:
   ```
   *.* @remote_server_ip:514
   ```
3. Restart the syslog service:
   ```
   sudo systemctl restart syslog
   ```

## Understanding and Using Syslog

Syslog is a standard protocol used for message logging in Unix-like systems. It allows separation of the software that generates messages, the system that stores them, and the software that reports and analyzes them.

### Syslog Facilities and Severity Levels

Syslog uses facilities and severity levels to categorize log messages:

**Facilities:**
- auth, authpriv, cron, daemon, kern, lpr, mail, mark, news, syslog, user, uucp, local0 through local7

**Severity levels (from highest to lowest):**
- emerg, alert, crit, err, warning, notice, info, debug

### Rsyslog Configuration

Debian uses rsyslog as its default syslog daemon. The main configuration file is `/etc/rsyslog.conf`.

Key configuration sections:

1. **Modules**: Load required modules for extended functionality.
2. **Global directives**: Set global options for rsyslog.
3. **Rules**: Define how messages are processed based on facility and severity.

Example rule:
```
auth,authpriv.* /var/log/auth.log
```
This rule sends all auth and authpriv messages to `/var/log/auth.log`.

### Customizing Syslog Rules

To create custom syslog rules:

1. Create a new configuration file in `/etc/rsyslog.d/`:
   ```
   sudo nano /etc/rsyslog.d/custom.conf
   ```
2. Add your custom rules, for example:
   ```
   :programname, iseqial, "myapp" /var/log/myapp.log
   ```
   This rule sends all logs from a program named "myapp" to `/var/log/myapp.log`.
3. Restart the rsyslog service:
   ```
   sudo systemctl restart rsyslog
   ```

### Syslog Security Considerations

1. **Log file permissions**: Ensure log files have appropriate permissions to prevent unauthorized access.
   ```
   sudo chmod 640 /var/log/syslog
   sudo chown syslog:adm /var/log/syslog
   ```
2. **Network security**: When using remote logging, consider using encryption (TLS) to protect log data in transit.
3. **Log retention**: Implement a log retention policy to balance storage requirements with compliance needs.
4. **Log integrity**: Use tools like logrotate to compress and sign rotated logs, ensuring their integrity.

# Optimizing System Performance

Optimizing your Debian system's performance involves fine-tuning various components to ensure efficient resource utilization and improved responsiveness.

## CPU Optimization

1. **CPU frequency scaling**: Adjust CPU frequency based on system load.
   - Install cpufrequtils:
     ```
     sudo apt install cpufrequtils
     ```
   - Set CPU governor to performance:
     ```
     sudo cpufreq-set -g performance
     ```
2. **Process niceness**: Adjust process priority using the `nice` and `renice` commands.
   ```
   nice -n 10 command_to_run
   sudo renice -n 10 -p process_id
   ```
