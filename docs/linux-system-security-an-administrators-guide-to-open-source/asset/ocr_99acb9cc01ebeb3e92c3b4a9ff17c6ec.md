secure if you do not allow nonsystem groups write permissions to system files and directories. Rik Farrow's book (cited in For Further Reading on page 379) discusses this in more detail.

So all vendors are smart and know this, right? Well, not all vendors ship their systems this way, and not all administrators care to make changes. This is a policy decision. Carefully review all the keywords in the tigerrc file and configure them to match the policy at your site. Then tiger's output will show you only the policy violations.

The distribution comes with several sample tigerrc files. The tigerrc- all file is configured to do all checks. You should copy one of the sample tigerrc files to tigerrc in the top level of your build directory and edit it to your taste. Some of the checks take longer to run than others. A list of keywords and values that you can use in a tigerrc file is shown in Table 13.6.

# Table 13.6 tigerrc Keywords, Values, and Descriptions

| Keyword | Value | Description |
| --- | --- | --- |
| Tiger_Check_PASSWD | Y or N | Enables or disables check of passwd file for problems (check_passwd script); usually runs quickly. |
| Tiger_Check_GROUP | Y or N | Enables or disables check of groups file (check_group script); usually runs quickly. |
| Tiger_Check_ACCOUNTS | Y or N | Enables or disables examination of password file and files in users' accounts for oddities (check_accounts script); time varies by number of users. |
| Tiger_Check_RHOSTS | Y or N | Enables or disables examination of users' .rhosts files for policy violations (check_rhosts script); time varies by number of users. |
| Tiger_Check_NETRC | Y or N | Enables or disables examination of users' .netrc files (check_netrc script); time varies by number of users. |
| Tiger_Check_ALIASES | Y or N | Enables or disables examination of system aliases files (check_aliases script); usually runs quickly. |
| Tiger_Check_CRON | Y or N | Enables or disables check of users' cron jobs (check_cron script); usually runs quickly. |
| Tiger_Check_MOTD | Y or N | Enables or disables check of the /etc/motd file for policy violations (check_motd script); usually runs quickly. |
| Tiger_Check_DOS | Y or N | Enables or disables examination of directory permissions and ownership for consistency with the policies (check_dos script). |
| Tiger_Check_FILES | Y or N | Enables or disables examination of world-readable files with the same owner as their directory for consistency with the policies (check_files script); usually runs quickly. |
| Tiger_Check_LINKS | Y or N | Enables or disables examination of symbolic and hard links for consistency with the policies (check_links script); usually runs quickly. |
| Tiger_Check_LOG | Y or N | Enables or disables examination of the log files for policy violations (check_log script); usually runs quickly. |
| Tiger_Check_SUIDSGID | Y or N | Enables or disables examination of SUID/SGID files for consistency with the policies (check_suidsgid script). |
| Tiger_Check_SHELLS | Y or N | Enables or disables examination of the /etc/shells file for consistency with the policies (check_shells script); usually runs quickly. |
| Tiger_Check_TMP | Y or N | Enables or disables examination of /tmp, /var/tmp, and /usr/tmp files for consistency with the policies (check_tmp script); usually runs quickly. |
| Tiger_Check_USERS | Y or N | Enables or disables examination of the /etc/passwd file for consistency with the policies (check_users script); usually runs quickly. |
| Tiger_Check_VERSION | Y or N | Enables or disables display of the Tiger version number (check_version script); usually runs quickly. |
| Tiger_Check_WARN | Y or N | Enables or disables display of warnings (check_warn script); usually runs quickly. |