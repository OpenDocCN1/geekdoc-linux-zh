![](bbox=[0.3, 0.08, 0.75, 0.24])

# **FIGURE 2.1**

> *The IP address has several parts that identify network granularity.*

Internet addressing has five basic address classes. Each class is a block of allocations for very large to small networks. The Internet addressing plan is organized so that companies may buy segments from the addressing space. The classes are labeled A–E:

| Class | Address | Address Range, Description |
| :--- | :--- | :--- |
| A | 0.0.0.0 to 0.255.255.255<br>1.0.0.0 to 126.255.255.255 | (Reserved) 2³²-2 or 16,777,214 nodes for each allocation segment. This class has 126 segments. Used in very large organizations that subnet as needed, such as Internet service providers (ISPs). |
| B | 127.0.0.0 to 127.255.255.255<br>128.XXX.0.0 to 191.XXX.255.255 | (Reserved for loopback interface) 2³⁰-2 or 65,534 nodes for each allocation segment. This class has 64×256 available segments. Used in large organizations such as companies and universities. They may create subnets. The XXX is the allocated and assigned subnet (for example, 129.5.0.0 is an allocated subnet). Note: This address space is almost used up. |
| C | 192.XXX.XXX.0 to 223.XXX.XXX.255 | 2⁸-2 or 254 nodes for each allocation segment. This class has 32×65,536 available segments. Small companies or individual. The address has several slots available here. |