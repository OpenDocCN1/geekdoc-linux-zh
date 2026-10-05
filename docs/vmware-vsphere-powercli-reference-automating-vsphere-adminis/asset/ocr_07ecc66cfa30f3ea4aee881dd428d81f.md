```
catch [Exception] {
    throw "Unable to back up VM $($CurrentVM.Name)";
}

end {
}
```

This function will perform the backup to the datastore provided, but you need to keep a few things in mind:

+   - The amount of disk space needed for the backup will be exactly the same as the current virtual machine's disks.
- No-duplication methods were applied to this backup. Third-party software could have made use of de-duplication, in which case the amount of data was stored significantly reduced.
- The backup file will be a complete copy of the virtual machine, which means if you were to power it on you would have an exact replica on the network, conflicting IP addresses, SID, and all!
- The script will not work if the VM has raw device mappings (RDMs) or independent disks.

In the next section, you will learn how to change the VM network settings en masse to help you double-check that your backups have completed successfully and that you have a working VM.

# Restore Your VMs from a DIY Backup

Having backed up your virtual machines using the code in Listing 11.1, you obviously will want to restore them at some point, even if it is just to verify a successful backup. At other times, you will want to use this technique to automate a move to an isolated network so that you can verify that a virtual machine boots correctly