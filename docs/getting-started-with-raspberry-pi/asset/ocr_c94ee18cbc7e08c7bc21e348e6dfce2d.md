+   2. PCMCIA client drivers need to associate their `pcmcia_device_id` table with their `probe()` and `remove()` methods. This tie up is achieved by the `pcmcia_driver` structure:

```
struct pcmcia_driver {
int (*probe)(struct pcmcia_device *dev); /* Probe
method */
void (*remove)(struct pcmcia_device *dev); /* Remove
method */
/* ... */
struct pcmcia_device_id *id_table; /* Device ID
table */
/* ... */
};
```

+   3. `struct pcmcia_device` internally represents a PCMCIA device and is defined as follows in `drivers/pcmcia/ds.h`:

```
struct pcmcia_device {
/* ... */
io_req_t io; /* I/O attributes */
irq_req_t irq; /* IRQ settings */
config_req_t conf; /* Configuration */
/* ... */
struct device dev; /* Connection to device model */
/* ... */
};
```

+   4. CIS manipulation routines use a `tuple_t` structure defined in `include/pcmcia/cis.h` to hold a CIS information unit. A `CISPL_LINK_MFC` tuple type, for example, contains information related to a multifunction card. For the full list of tuples and their descriptions, look at `include/pcmcia/cis.h` and http://pcmcia-cs.sourceforge.net/ftp/doc/PCMCIA-PROG.html.

```
typedef struct tuple_t {
/* ... */
cisdata_t TupleCode; /* See
`include/pcmcia/cis.h` */
/* ... */
cisdata_t DesiredTuple; /* Identity of the desired
tuple */
/* ... */
cisdata_t *TupleData; /* Buffer space */
};
```

+   5. The CIS contains configuration table entries for each configuration that the card supports. `cispl_cftable_entry_t`, defined in `include/pcmcia/cis.h`, holds such an entry:

```
typedef struct cispl_cftable_entry_t {
/* ... */
cispl_power_t vcc, vppi, vpp2; /* Voltage level */
cispl_io_t io; /* I/O attributes */
cispl_irq_t irq; /* IRQ settings */
cispl_mem_t mem; /* Memory window */
/* ... */
};
```