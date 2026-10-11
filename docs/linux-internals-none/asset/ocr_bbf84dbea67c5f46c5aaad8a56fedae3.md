# Linux Kernel Base Functions



```
78
zone t node_zones[MAX_NR_ZONES];
79
zonelist t node_zonelist[NR_GFPINDEX];
80
struct page *node_mem_map;
81
unsigned long *valid_addr_bitmap;
82
struct bootmem_data *bdata;
83
unsigned long node_start_paddr;
84
unsigned long node_start_mapnr;
85
unsigned long node_size;
86
int node_id;
87
} pg_data t;
88
extern int numnodes;
89
90
#define memclass (pgzone, tzone) (((pgzone)->zone_pgdat == (tzone)->zone_pgdat)
91
\
92
&& (((pgzone) - (pgzone)->zone_pgdat->node_zones) <= \
93
((tzone) - (pgzone)->zone_pgdat->node_zones)))
94
95
/*
96
* The following two are not meant for general usage. They are here as
97
* prototypes for the discontig memory code.
98
*/
99
extern void show_free_areas core (int);
100
extern void free_area_init core (int nid, pg_data t *pgdat, struct page **gmap,
101
unsigned long *zones_size, unsigned long paddr);
102
103
#ifndef CONFIG_DISCONTIGMEM
104
105
extern pg_data t contig_page_data;
106
107
#define NODE_DATA(nid)
108
(
&contig_page_data)
109
#define NODE_MEM_MAP(nid)
110
mem_map
111
112
#else /* !CONFIG_DISCONTIGMEM */
113
114
#include <asm/mmzone.h>
115
116
#endif /* !CONFIG_DISCONTIGMEM */
117
118
#define MAP_ALIGN(x)
119
((((x) % sizeof (mem_map_t)) == 0)? (x) : ((x) + \
120
sizeof (mem_map_t) - ((x) % sizeof (mem_map_t))))
121
122
#endif /* !__ASSEMBLY__ */
123
#endif /* __KERNEL__ */
124
#endif /* __LINUX_MMZONE_H */
125
```

# Data Structures—linux/timer.h

```
1
#ifndef LINUX_TIMER_H
2
#define LINUX_TIMER_H
3
```