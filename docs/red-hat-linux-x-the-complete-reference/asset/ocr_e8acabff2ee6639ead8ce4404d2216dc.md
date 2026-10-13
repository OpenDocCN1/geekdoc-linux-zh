the **accept** and **reject** commands start and stop particular jobs. **lpinfo** provides information about printers, and **lpoptions** lets you set printing options. The **lpadmin** command lets you perform administrative tasks like adding printers and changing configurations. CUPS administrative tools are listed in Table 25-3.

# lpadmin

You can use the **lpadmin** command to either set the default printer or configure various options for a printer. You can use the **-d** option to specify a particular printer as the default destination (you can also do this in redhat-config-printer). Here **myepson** is made the default printer:

```
lpadmin -d myepson
```

Table 25-3: CUPS Administrative Tools

| Administration Tool | Description |
|---|---|
| lpadmin | CUPS printer configuration |
| lpoptions | Set printing options |
| enable | Activate a printer |
| disable | Stop a printer |
| accept | Allows a printer to accept new jobs |
| reject | Prevents a printer from accepting print jobs |
| lpinfo | List CUPS devices available |

The **-p** option lets you designate a printer for which to set various options. The following example sets printer description information:

```
lpadmin -p myepson -D Epson550
```

Certain options let you control per-user quotas for print jobs. The **job-k-limit** sets the size of a job allowed per user, **job-page-limit** sets the page limit for a job, and the **job-quota-period** limits the number of jobs with a specified time frame. The following command set a page limit of 100 for each user.

```
lpadmin -p myepson -o job-page-limit=100
```

User access control is determined with the **-u** option with an **allow** or **deny** list. Users allowed access are listed following the **allow:** entry, and those denied access are listed with a **deny:** entry. Here access is granted to **chris** but denied to **aleina** and **larisa**.

```
lpadmin -p myepson -u allow:chris deny:aleina,larisa
```

Use **all** or **none** to permit or deny access to all or no users. You can create exceptions by using **all** or **none** in combination with user-specific access. The following example allows access to all users except **justin**:

```
lpadmin -p myepson -u allow:all deny:justin
```

# lpoptions

The **lpoptions** command lets you set printing options and defaults that mostly govern how your print jobs will be printed. For example, you can set the color or page format to be used with a particular printer. Default settings for all users are maintained by the root user in the **/etc/cups/lpoptions** file, and each user can create their own configurations, which are saved in their **.lpoptions** files. The **-l** option lists current options for a printer, and the **-p** option designates a printer (you can also set the default printer to use with the **-d** option).

```
lpoptions -p myepson -l
```