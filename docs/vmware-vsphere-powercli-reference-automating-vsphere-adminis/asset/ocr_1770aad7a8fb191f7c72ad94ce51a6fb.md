# CHAPTER 14  • MAINTAIN SECURITY IN VSPHERE ENVIRONMENT

Let's take an example where you need to prepare a list of patches to apply to ESXi 5.5 servers during the next patching window. Where the vSphere Update Manager Client, you can access information, but there is no way to extract it for a distributed-report.

Retrieve this same information using the Get-Compliance cmdlet, retrieve data from a host that has the baseline in question and scanned. In particular, look at the NotCompliantPatches. Then, select the properties you wish to export for the report, including a calculated property named Version, and export the results to a CSV file (Listing 14.20).

# LISTING 14.20 Generating a detailed noncompliant report for a host

```
(Get-Compliance -Entity esxi01 -Detailed).NotCompliantPatches
Select-Object Name, IDByVendor, Description, @(N='Version';=$_.Product.Version),ReleaseDate
Export-Csv patches.csv -NoTypeInformation -UseClause
```

The information produced in our result is displayed in Figure 14.5.

# FIGURE 14.5 Noncompliant patches in detail

| Name | IDByVendor | /description | Version | ReleaseDate |
|---|---|---|---||}{
| 1 Update-esxi01 | ESX-201402861-BG | For more information, see http://kb.vmware.com/article/207923 | 5.5 | 02/12/2014 00:00 |
| 2 Update-esxi02 | ESX-201404770-BG | For more information, see http://kb.vmware.com/article/207795 | 5.5 | 04/10/2014 00:00 |
| 3 Update-esxi03 | ESX-201405161-BG | For more information, see http://kb.vmware.com/article/207829 | 5.5 | 05/13/2014 00:00 |
| 4 Update-esxi04 | ESX-201405581-BG | For more information, see http://kb.vmware.com/article/207915 | 5.5 | 05/21/2014 00:00 |
| 5 Update-esxi05 | ESX-201406381-BG | For more information, see http://kb.vmware.com/article/207963 | 5.5 | 06/15/2014 00:00 |
| 6 Update-safe-ahci | ESX-201407131-BG | For more information, see http://kb.vmware.com/article/208012 | 5.5 | 07/11/2014 00:00 |
| 7 Update-esxi06 | ESX-201407531-BG | For more information, see http://kb.vmware.com/article/208037 | 5.5 | 07/25/2014 00:00 |
| 8 Update-tools-light | ESX-201408481-BG | For more information, see http://kb.vmware.com/article/208063 | 5.5 | 08/19/2014 00:00 |
| 9 Update-esxi07 | ESX-201409111-BG | For more information, see http://kb.vmware.com/article/208111 | 5.5 | 09/09/2014 00:00 |
| 10 Update-esxi-5.5-linux-beta | ESX-201409501-BG | For more information, see http://kb.vmware.com/article/208159 | 5.5 | 09/23/2014 00:00 |
| 11 Update-esxi-5.5-linux-kernel | ESX-201410231-BG | For more information, see http://kb.vmware.com/article/208219 | 5.5 | 10/14/2014 00:00 |
| 12 Update-esxi-5.5-tools-gui | ESX-201410731-UI | For more information, see http://kb.vmware.com/article/208277 | 5.5 | 10/31/2014 00:00 |
| 13 Update-esxi-5.5-misc-drivers | ESX-201411529-UG | For more information, see http://kb.vmware.com/article/208302 | 5.5 | 11/27/2014 00:00 |
| 14 Update-esxi-5.5-tools-cli | ESX-201411931-UI | For more information, see http://kb.vmware.com/article/208395 | 5.5 | 12/10/2014 00:00 |
| 15 Update-esxi-5.5-complete-2 | ESX-201412632-BE | For more information, see http://kb.vmware.com/article/208471 | 5.5 | 12/25/2014 00:00 |
| 16 Uninstall-linux-kernel | ESX-201305751-VA | For more information, see http://kb.vmware.com/article/207174 | 4.5 | 05/19/2014 00:00 |

# Applying Patches with vSphere Update Manager

In this chapter we have covered automated patching via vSphere Update Manager. However, for some reasons vSphere Update Manager might not be available. If that is the case, there are two methods that you can use: For patches in CSV format, you can use the PowerCLI cmdlet Get-VMHostPatch. For VIB files, you can use PowerCLI's implementation of the ESXi command-line tool, escli.