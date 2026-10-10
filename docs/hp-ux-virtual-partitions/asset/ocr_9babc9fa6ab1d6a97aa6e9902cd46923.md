| 13:18:04 | 60 | 5 | 3 | 33 |
| :--- | :--- | :--- | :--- | :--- |
| 13:19:04 | 77 | 3 | 4 | 16 |
| 13:20:04 | 76 | 5 | 3 | 15 |

| 14:30:04 | 50 | 6 | 6 | 38 |
| :--- | :--- | :--- | :--- | :--- |
| 14:31:04 | 57 | 12 | 19 | 12 |
| 14:32:04 | 51 | 8 | 20 | 21 |
| 14:33:04 | 41 | 4 | 9 | 46 |
| 14:34:04 | 43 | 4 | 9 | 45 |
| 14:35:04 | 38 | 4 | 6 | 53 |
| 14:36:04 | 38 | 9 | 7 | 46 |
| 14:37:04 | 46 | 3 | 11 | 40 |
| 14:38:04 | 43 | 4 | 7 | 46 |
| 14:39:04 | 37 | 4 | 5 | 54 |
| 14:40:04 | 33 | 4 | 5 | 58 |
| 14:41:04 | 40 | 3 | 3 | 53 |
| 14:42:04 | 44 | 3 | 3 | 50 |
| 14:43:04 | 27 | 3 | 7 | 64 |
| Average | 57 | 5 | 8 | 30 |

# **sar -b**

Report buffer cache activity. A database application such as Oracle would recommend that you use this option to see the effectiveness of buffer cache use. You extract the binary data saved in a file to get CPU information, as shown in the following example:

```
# sar -b -f /tmp/sar.data
Header information for your system

12:52:04 breads/s freads/s wroache lwrite/s lwrit/s wreache pread/s pwrite/s
12:53:04 5 608 38 1 11 95 0 0
12:54:04 7 759 99 0 14 99 0 0
12:55:04 2 1733 166 4 24 83 0 0
12:56:04 1 836 100 1 18 96 0 0
12:57:04 0 623 100 2 21 92 0 0
12:58:04 0 779 100 1 16 94 0 0
12:59:04 0 1125 100 0 14 98 0 0
13:00:04 2 1144 100 9 89 89 0 0
13:01:04 10 899 99 11 76 86 0 0
13:02:04 0 1156 100 0 14 99 0 0
13:03:04 1 578 100 2 12 88 0 0
13:04:04 5 1251 100 0 12 99 0 0
```