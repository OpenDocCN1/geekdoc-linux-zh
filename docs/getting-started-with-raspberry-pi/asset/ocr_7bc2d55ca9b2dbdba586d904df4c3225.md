524

# Chapter 20. More Devices and Drivers

```
edac_mc_handle_ue(mci, info->eap, 0, row, "i855 UE");

} else if (is_SBE()) { /* is_SBE() looks at i855_ERRSTS_REGISTER and checks
for an SBE. Implementation not shown */

edac_mc_handle_ce(mci, info->eap, 0, info->derrsyn, row, 0,
"i855 CE");
}

return 1;
}

/* This method is registered with the EDAC core from i855_probe() */

static void
i855_check(struct mem_ctl_info *mci)
{

struct i855_error_info info;

i855_get_error_info(mci, &info);
i855_process_error_info(mci, &info, 1);
}

/* The PCI driver probe method, part of the pci_driver structure */

static int
i855_probe(struct pci_dev *pdev, int dev_idx)
{

struct mem_ctl_info *mci;

/* ... */
pci_enable_device(pdev);

/* Allocate control memory for this memory controller.
The 3 arguments to edac_mc_alloc() correspond to the
amount of requested private storage, number of chip-select
rows, and number of channels in your memory layout */

mci = edac_mc_alloc(0, CSROWS, CHANNELS);

/* ... */

mci->edac_check = i855_check; /* Supply the check method to the
EDAC core */

/* Do other memory controller initializations */

/* ... */

/* Register this memory controller with the EDAC core */

edac_mc_add_mc(mci, 0);

/* ... */
}

/* Remove method */

static void __devexit
i855_remove(struct pci_dev *pdev)
{

struct mem_ctl_info *mci = edac_mc_find_mci_by_pdev(pdev);

if (mci && !edac_mc_del_mc(mci)) {

edac_mc_free(mci); /* Free memory for this controller. Reverse
of edac_mc_alloc() */
}
}

/* PCI Device ID Table */

static const struct pci_device_id i855_pci_tbl[] __devinitdata = {
{PCI_VEND_DEV(INTEL, I855_PCI_DEVICE_ID),
PCI_ANY_ID, PCI_ANY_ID, 0, 0},
```