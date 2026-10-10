In this example, the first 16 bits (128.8) represent the network number, and the remainder (27.18) represent the specific host number. This network number can contain up to 65,536 hosts (the same as a Class B address). The following list shows how many hosts can be represented in networks using different numbers to identify the network:

+   - /0 4,294,967,296 hosts
+   - /1 2,147,483,648 hosts
+   - /2 1,073,741,824 hosts
+   - /3 536,870,912 hosts
+   - /4 268,435,456 hosts
+   - /5 134,217,728 hosts
+   - /6 67,108,864 hosts
+   - /7 33,554,432 hosts
+   - /8 16,777,216 hosts
+   - /9 8,388,608 hosts
+   - /10 4,194,304 hosts
+   - /11 2,097,152 hosts
+   - /12 1,048,576 hosts
+   - /13 524,288 hosts
+   - /14 262,144 hosts
+   - /15 131,072 hosts
+   - /16 65,536 hosts
+   - /17 32,768 hosts
+   - /18 16,382 hosts
+   - /19 8,192 hosts
+   - /20 4,096 hosts
+   - /21 2,048 hosts
+   - /22 1,024 hosts
+   - /23 512 hosts
+   - /24 256 hosts
+   - /25 128 hosts
+   - /26 64 hosts
+   - /27 32 hosts
+   - /28 16 hosts
+   - /29 8 hosts
+   - /30 4 hosts
+   - /31 2 hosts
+   - /32 1 host

The CIDR addressing scheme also helps reduce the routing overload problem by having a single, high-level route represent many lower-level routes. For example, an ISP could be assigned a single /13 IP network and assign the 500,000-plus addresses to its customers. Routers outside the ISP would only need to know how to reach the ISP for those half-million addresses. The ISP would then be responsible for maintaining routing information for all of the host routes with that network address.