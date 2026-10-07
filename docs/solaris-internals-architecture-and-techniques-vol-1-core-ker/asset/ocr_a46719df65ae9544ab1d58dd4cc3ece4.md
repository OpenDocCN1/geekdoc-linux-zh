# Memory Segments

151

![](bbox=[0.115, 0.097, 0.913, 0.506])

Figure 5.11 mmap Shared Mapped Files

Table 5-5 Shared Mapped Mapped File Flags

| Flag | Protection Mode | Result |
| --- | --- | --- |
| MAP_SHARED | PROT_READ PROT_WRITE | Modifications are reflected among all processes sharing the mapping. |
| MAP_PRIVATE | PROT_READ PROT_WRITE | Modifications are seen only by the process mapping the file. The copy-on-write process creates a page of anonymous memory and gives a private copy to the process. |