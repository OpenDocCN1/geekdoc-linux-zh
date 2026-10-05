# CHAPTER 21

Realize Orchestrator (vRO) (formerly vCenter Orchestrator) has been bundled part of vCenter deployments for a long time but was known as one of VMware's 'best-kept secrets'. Those who know about it and used it were able to take advantage of its ability to simplify the automation of complex IT tasks, both with VMware and third-party products, by the creation of workflows. Recent integration with vRealize Automation Center (formerly vCloud Automation Center) has a significant increase in popularity and use. We will explore some of the ways to use PowerShell with vRO, to cover many scenarios where vRO is not natively able to integrate with external systems or where the native integration has some drawbacks.

# Requirements

If you want to integrate vRO, there are a number of requirements over and above those for a base vRO configuration. They are detailed in the following sections.

# vRO

vRO 6.0 is available in two flavors similar to vCenter: a Linux-based appliance or a Windows-based installation process. For the purposes of this book, we will be using the Windows-based installation, since we will be demonstrating not only the use of the official vRO PowerShell plug-in, but also an alternative method-based that bypasses the plug-in. The alternative method requires the use of a Windows-based vRO system. We will be using Windows Server 2012 R2 for the base OS. A list of supported Windows operating systems for vRO can be found here: http://kb.vmware.com/kb209273.

# PowerShell

PowerShell v4 is part of the base OS in Windows Server 2012 R2. The vRO PowerShell plug-in version 1.0.4 supports PowerShell v4.

> Prior to vRO 5.5.2, the PowerShell plug-in was in a separately installed plug-in that needed to be added post-vRO deployment. Since vRO 5.5.2, the PowerShell plug-in has been shipped as part of the vRO deployment. We are using vRO 6.0 in this book and consequently will not be covering how to install the separate plug-in used in earlier versions.

![](bbox=[0.253, 0.763, 0.311, 0.803])