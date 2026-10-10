The output of the products and subproducts levels is the same; therefore, there are no subproducts in GlancePlus/UX. We can go one step further and take this to the fileset level, as shown in the following example:

```
$ swlist -1 filesent B3701AA.TRY
# various header information
#...
#...
B3701AA.TRY B.11.05.1 Tr�al HP GlancePlus/UX Pak for $800 11.00
B3701AA.TRY,MeasurementInt B.11.00.1 HP-UX Measurement Interface for 11.00
B3701AA.TRY,MeasurementInt,ARM B.11.00.1 MP-UX Application Response Measurement for 11.00
B3701AA.TRY,MeasurementInt,MI B.11.00.1 HP-UX Measurement Interface for 11.00
B3701AA.TRY,MeasureWare B.11.00.1 MeasureWare Software/UX
B3701AA.TRY,MeasureWare,MWA B.11.00.1 MeasureWare Software files
B3701AA.TRY,MeasureWare,MWANQ B.11.00.1 MeasureWare NQS Connectivity Module
Software files B.11.00.1 HP PDS Data Source Integration
B3701AA.TRY,MeasureWare,PERFDSC B.11.00.1 HP GlancePlus/UX
B3701AA.TRY,Glance B.11.00.1 HP GlancePlus files
B3701AA.TRY,Glance,GLANC B.11.00.1 HP GlancePlus Motif interface files
B3701AA.TRY,Glance,GPM (bundle) (product) (filesent)
```

![](bbox=[0.06, 0.5, 0.15, 0.58])

With the `swlist` command and the `-1` option, we have worked our way down the hierarchy of HP GlancePlus/UX. Going down to the file level with the `-1 file` option produces a long list of files associated with this product. Table 1-2 shows some of the `-1` options to `swlist` that I use:

# TABLE 1-2 List of Some swlist -1 Options

| Command | Explanation |
| --- | --- |
| `swlist -r root` | Shows the root level. |
| `swlist -1 sroot` | Shows the shared roots. |
| `swlist -1 proot` | Shows the private roots. |
| `swlist -1 bundle` | Shows bundles only. |
| `swlist -1 product` | Shows products only. |
| `swlist -1 subproduct` | Shows both products and subproducts. |
| `swlist -1 filesent` | Shows products, subproducts, and filesets. |
| `swlist -1 file` | Shows products, subproducts, filesets, files and numbers. |
| `swlist -1 category` | Shows all categories of available patches if they have category in their definition. |
| `swlist -1 patch` | Shows all applied patches. |