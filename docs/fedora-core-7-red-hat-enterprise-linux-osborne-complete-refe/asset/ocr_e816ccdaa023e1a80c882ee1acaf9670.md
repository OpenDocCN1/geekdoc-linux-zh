| Administration Tool | Description |
| :--- | :--- |
| lpadmin | CUPS printer configuration |
| lpoptions | Set printing options |
| enable | Activate a printer |
| disable | Stop a printer |
| accept | Allow a printer to accept new jobs |
| reject | Prevent a printer from accepting new print jobs |
| lpinfo | List CUPS devices available |

**TABLE 26-4** CUPS Administrative Tools

# # lpadmin

You can use the **lpadmin** command to either set the default printer or configure various options for a printer. You can use the **-d** option to specify a particular printer as the default destination (you can also do this in **system-config-printer**). Here **mypepson** is made the default printer:

```
lpadmin -d mypepson
```

The **-p** option lets you designate a printer for which to set various options. The following example sets printer description information:

```
lpadmin -p mypepson -D Epson550
```

Certain options let you control per-user quotas for print jobs. The **job-k-limit** option sets the size of a job allowed per user, **job-page-limit** sets the page limit for a job, and **job-quota-period** limits the number of jobs within a specified time frame. The following command set a page limit of 100 for each user:

```
lpadmin -p mypepson -o job-page-limit=100
```

User access control is determined with the **-u** option with an **allow** or **deny** list. Users allowed access are listed following the **allow** entry, and those denied access are listed with a **deny**: entry. Here access is granted to **chris** but denied to **aleina** and **larisa**.

```
lpadmin -p mypepson -u allow:chris deny:aleina,larisa
```

Use **all** or **none** to permit or deny access to all or no users. You can create exceptions by using **all** or **none** in combination with user-specific access. The following example allows access to all users except **justin**:

```
lpadmin -p mypepson -u allow:all deny:justin
```

![](bbox=[0.92, 0.635, 1.0, 0.74])