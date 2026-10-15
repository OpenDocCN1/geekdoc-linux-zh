
``` 
1 cdl_configuration eCos {
2   description "";
3
4   # These fields should not be modified.
5   hardware pc;
6   template net;
7   package -hardware CYPGHAL_HAL_I386 current ;
8   package -hardware CYPGHAL_HAL_I386_GENERIC current ;
9   package -hardware CYPGHAL_HAL_I386_PC current ;
10  package -hardware CYPGHAL_HAL_I386_PCMB current ;
11
12
13
14  package -template CYPGHAL_HAL current ;
15  package -template CYPGHAL_IO current ;
16  package -template CYPGHAL_IO_SERIAL current ;
17  package -template CYPGHAL_INFRA current ;
18  package -template CYPGHAL_ISOINFRA current ;
19  package -template CYPGHAL_KERNEL current ;
20  package -template CYPGHAL_ERROR current ;
21  package -template CYPGHAL_IO_FILEIO current ;
22  package -template CYPGHAL_NET current ;
23  package -template CYPGHAL_IO_ETH_DRIVERS current ;
24  };
25
26
27  cdl_option CYGNUM_HAL_COMMON_INTERRUPTS_STACK_SIZE {
29    # Flavor: data
30    user_value 4096
31    # value_source
32    # Default value: CYPGHAL_KERNEL 32768
33    # CYPGHAL_KERNEL (unknown)
34    # 32768
35    # Legal values: 1024 to 10576
36 }
```
