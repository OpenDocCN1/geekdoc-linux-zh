
`chmod +x /path/to/backup_script.sh`

then edit our cron table

`crontab -e`

`30 23 * * 6 /path/to/backup_script.sh`
