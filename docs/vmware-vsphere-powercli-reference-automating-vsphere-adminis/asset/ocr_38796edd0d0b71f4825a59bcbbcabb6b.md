# CHAPTER 7 • USING TEMPLATES AND CUSTOMIZATION SPECIFICATIONS

> NOTE Prior to Virtual Center 2.5 update 2, you had to power off the virtual machine to clone to a template. Every version since then simply takes a snapshot and clones from that snapshot if the VM is powered on. Although this approach works, it might not result in a usable template, so proceed with caution.

The latest release of vSphere came a new construct called a content library. Content libraries provide a centralized store to hold Open Virtualization Format OVF), template, and International Organization for Standardization (ISO) files. When a template is stored in the content library, the library can handle rudimentary replication between vCenter instances. Unlike traditional templates, a template stored in a content library is stored as an OVF file. This means that it cannot be easily converted back to a VM without being deployed. Although this new capacity has massive potential, as of writing it has not been fully integrated into PowerCLI. The content library itself can be managed, but VM provisioning are not enabled in the built-in cmdlets.

That's all there is to it from vCenter Server/PowerCLI point of view. The truth about templates is that they are only as good as the source VM—which means all the hard work is done up in guest.

# Deploying Guests from Templates

With the required templates pre-staged, it's time to deploy some guests. Deploying from a template is a clone operation, and is accomplished in Chapter 6, "Creating Virtual Machines," is accomplished via the New-VM cmdlet. The short script in Listing 7.9 deploys a web server from the Windows 2012 R2 template to Listing 7.1.

# LISTING 7.9 Deploying a guest from a template

```
$Template = Get-Template -Name 'WS2012R2'
$VMHost = Get-VMHost -Name 'vSphere'
$New-VM -Template $Template -Name 'WEB001' -VMHost $VMHost
```

A straight deploy operation is a very simple task, but the problem is that everything must be prepared prior to the creation of the template because the resulting VM will be an exact copy of the template. Technically, there is nothing wrong with this approach. Mature Windows/Linux shops that have their own deployment processes nailed down aren't interested in any assistance from VMware. Individuals fortunate