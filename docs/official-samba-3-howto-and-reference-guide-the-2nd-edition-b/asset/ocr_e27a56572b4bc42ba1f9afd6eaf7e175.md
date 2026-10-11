Dependentfiles: [\\10.160.50.8\\print$\\W32X86\\WBAPI.DLL]
Dependentfiles: [\\10.160.50.8\\print$\\W32X86\\NBIPC.DLL]
Dependentfiles: [\\10.160.50.8\\print$\\W32X86\\cns3gum.dll]

Monitorname: [CPCA Language Monitor2]
Defaultdatatype: []

If we write the “version 2” files and the “version 3” files into different text files and compare the result, we see this picture:

```
root# sdiff 2-files 3-files
```

```
cns3g.dll                             cns3g.dll
iR8500sg.xpd                        iR8500sg.xpd
cns3gui.dll                         cns3gui.dll
cns3g.hlp                           cns3g.hlp
AUCPLMNT.DLL                        | aucplmNT.dll
> ucs32p.dll
> tn132.dll

aussdrv.dll                         aussdrv.dll
cnspdc.dll                          cnspdc.dll
aussapi.dat                         aussapi.dat
cns3407.dll                         cns3407.dll
CnS3G.cnt                           CnS3G.cnt
NBAPI.DLL                           NBAPI.DLL
NBIPC.DLL                           NBIPC.DLL
cns3gum.dll                         | cpcview.exe
> cpcdsp1.exe
> cpcqm.exe
> cpcspl1.dll
> cfine32.dll
> cpcr407.dll
> Cpcqm407.hlp
> cpcqm407.cnt
> cns3ggr.dll
```

Do not be fooled! Driver files for each version with identical names may be different in their content, as you can see from this size comparison:

```
root# for i in cns3g.hlp cns3gui.dll cns3g.dll; do
    smbclient \\/10.160.50.8/print/$ -U 'Administrator/\'x\'xxxx\'' \
        -c "cd W32X86/3; dir $i; cd .. ; cd 2; dir $i"; \
```