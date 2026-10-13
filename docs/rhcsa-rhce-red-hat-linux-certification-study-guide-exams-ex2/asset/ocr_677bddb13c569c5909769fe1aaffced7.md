# FIGURE 16-3 NFS-related SELinux boolean options

![](bbox=[0.12, 0.22, 0.9, 0.6])

they're worth repeating, if only to help those who fear SELinux. The first module is not shown in Figure 16-3. The remaining modules are described in the order shown in the figure.

+   - **allow_gssd_read_tmp** Supports the reading of temporary directories by the General Security Services daemon, gssd, which helps protect NFS when systems authenticate through Kerberos 5.
+   - **httpd_use_nfs** Supports access to shared NFS directories by the Apache Web server.
+   - **cd_record_read_content** Enables access to mounted NFS directories by the cdrecord command.
+   - **allow_ftpd_use_nfs** Allows the use of shared NFS directories by FTP servers.
+   - **git_system_use_nfs** Supports access of NFS shares by the git revision control system service.
+   - **nfs_export_all_ro** Supports read-only access to shared NFS directories.
+   - **nfs_export_all_rw** Supports read/write access to shared NFS directories.