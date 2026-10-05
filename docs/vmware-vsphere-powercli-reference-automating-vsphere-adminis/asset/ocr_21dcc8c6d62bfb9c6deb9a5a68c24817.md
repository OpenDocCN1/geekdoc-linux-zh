# Understanding Datacenter Compliance

The VUM set of cmdlets includes Get-Compliance, which allows you to report on
host and VM compliance against their attached baselines. You can run this cmdlet\against a top-level datacenter object and generate a report for all hosts and VMs of
their compliance status against any attached baseline.

> If you run the cmdlet against a top-level datacenter object, it will take a long time
to run—particularly if the count of objects within the datacenter is in the hundreds or
thousands.

Execute the code in Listing 14.14 to generate a compliance report for all hosts and
VMs in Prod01.

# LISTING 14.14 Generating a compliance report

```
Get-Compliance -Entity (Get-Datacenter 'Prod01')
```

Get-Compliance returns a compliance status result for each attached baseline. So if
multiple baselines are attached, there will be multiple rows for that host or
virtual machine. Sample output will be the lines of the following:

| Entity | Baseline | Status |
|---|---|---|
| VM01 | VMware Tools Upgrade to Match Host | Compliant |
| VM01 | VM Hardware Upgrade to Match Host | NotCompliant |
| VM02 | VMware Tools Upgrade to Match Host | Compliant |
| VM02 | VM Hardware Upgrade to Match Host | NotCompliant |
| vesxi055 | ESXI 5.5 - Current | NotCompliant |
| vesxi106 | ESXI 5.5 - Current | Compliant |

This of course, was output to the PowerShell console. Most likely, you are required
to produce a more typical report format as CSV or XML. To do so, select the
properties required for your report and use one of the PowerShell cmdlets,
like Export-CSV, to generate the final report, as we did:

```
Get-Compliance -Entity (Get-Datacenter 'Prod01') |
Select-Object Entity, Baseline, Status |
Export-CSV ComplianceStatus.csv -NoInformation -UseCulture
```