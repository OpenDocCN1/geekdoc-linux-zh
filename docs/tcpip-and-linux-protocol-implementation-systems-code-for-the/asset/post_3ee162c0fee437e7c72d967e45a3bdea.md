
# List of Figures

- 5.139 TCP state variables: linux/include/net/tcp.h 198
- 5.140 Socket state i, start: linux/include/net/sock.h 199
- 5.141 Socket relevant IP option state: linux/include/net/sock.h 199
- 5.142 IPv6 state: linux/include/net/sock.h 200
- 5.143 Socket state i, demultiplex data: linux/include/net/sock.h 201
- 5.144 Socket state ii, resource data: linux/include/net/sock.h 201
- 5.145 Socket state iii, socket itself: linux/include/net/sock.h 201
- 5.146 Socket state iv, routing, and filtering: linux/include/net/sock.h 202
- 5.147 Socket state v, protects protocol info: linux/include/net/sock.h 203
- 5.148 Socket state vi, timers and callbacks: linux/include/net/sock.h 204
- 5.149 Socket state vii, timers and callbacks: linux/include/net/sock.h 205
- 5.150 Proposal to tidy up socket state: linux/include/net/sock.h 205
- 5.151 Socket reference counting management: linux/include/net/sock.h 206
- 5.152 Inline functions for socket reference management: linux/include/net/sock.h 207
- 5.153 Inline functions for socket reference management: linux/include/net/sock.h 207
- 5.154 Inline functions for socket reference management: linux/include/net/sock.h 208
- 5.155 Socket route state management: linux/include/net/sock.h 208
- 5.156 Socket route state management: linux/include/net/sock.h 209
- 5.157 Socket route state management: linux/include/net/sock.h 210
- 5.158 Socket queue management interface: linux/include/net/sock.h 210
- 5.159 Socket queue management interface: linux/include/net/sock.h 211
- 5.160 Socket queue management interface: linux/net/core/scm.h 211
- 5.161 Socket credential function: linux/include/net/sock.h 212
- 5.162 Socket credential interface: linux/include/net/sock.h 212
- 5.163 BSD producer/consumer-transport out 213
- 6.164 BSD producer/consumer-network out 213
- 5.165 BSD producer/consumer-chain-legend 214
- 6.1 IP output-add header and sender: linux/net/ipv4/ip.output.c 215
- 6.2 IP output-finish sending (note-two process): linux/net/ipv4/ip.output.c 216
- 6.3 Internet Protocol-checksum: linux/net/ipv4/ip.output.c 217
- 6.4 IP output-loopback: linux/net/ipv4/ip.output.c 218
- 6.5 IP output-reroute?: linux/net/ipv4/ip.output.c 218
- 6.6 IP output-multicast replication: linux/net/ipv4/ip.output.c 219
- 6.7 IP output-multicast replication: linux/net/ipv4/ip.output.c 219
- 6.8 IP output-drive output: linux/net/ipv4/ip.output.c 219
- 6.9 IP output-queue for sending-part 2i: linux/net/ipv4/ip.output.c 219

| 6.10 | IP output-queue for sending-part 2: linux/net/ipv4/ip.output.c | 220 |
| 6.11 | IP output-queue packet for sending—part 1: linux/net/ipv4/ip.output.c | 221 |
| 6.12 | IP output-queue packet for sending—part 1: linux/net/ipv4/ip.output.c | 221 |
| 6.13 | IP output—classic building of IP packet: linux/net/ipv4/ip.output.c | 222 |
| 6.14 | IP output—classic building of IP packet: linux/net/ipv4/ip.output.c | 223 |
| 6.15 | IP output—classic building of IP packet: linux/net/ipv4/ip.output.c | 223 |
| 6.16 | IP output—classic building of IP packet: linux/net/ipv4/ip.output.c | 224 |
| 6.17 | IP output—classic building of IP packet: linux/net/ipv4/ip.output.c | 224 |
| 6.18 | IP output—classic building of IP packet: linux/net/ipv4/ip.output.c | 225 |
| 6.19 | IP output—classic building of IP packet: linux/net/ipv4/ip.output.c | 225 |
| 6.20 | IP output—classic building of IP packet: linux/net/ipv4/ip.output.c | 226 |
| 6.21 | IP output—classic building of IP packet: linux/net/ipv4/ip.output.c | 226 |
| 6.22 | IP output—fast path for nonfragmented packets: linux/net/ipv4/ip.output.c | 227 |
| 6.23 | IP output—fast path for nonfragmented packets: linux/net/ipv4/ip.output.c | 228 |
| 6.24 | IP output—fast path for nonfragmented packets: linux/net/ipv4/ip.output.c | 229 |
| 6.25 | IP output—fragment: linux/net/ipv4/ip.output.c | 229 |
| 6.26 | IP output—fragment: linux/net/ipv4/ip.output.c | 230 |
| 6.27 | IP output—fragment: linux/net/ipv4/ip.output.c | 230 |
| 6.28 | IP output—fragment: linux/net/ipv4/ip.output.c | 231 |
| 6.29 | IP output—fragment: linux/net/ipv4/ip.output.c | 232 |
| 6.30 | IP output—deal with ove and checksum for next function: linux/net/ipv4/ip.output.c | 233 |
| 6.31 | IP output—build a packet that is response to something: linux/net/ipv4/ip.output.c | 233 |
| 6.32 | IP output—initialize IP layer: linux/net/ipv4/ip.output.c | 234 |
| 6.33 | Internet Protocol—input—preamble: linux/net/ipv4/ip.input.c | 235 |
| 6.34 | IP input—stra for network managers: linux/net/ipv4/ip.input.c | 235 |
| 6.35 | IP input—router handler: linux/net/ipv4/ip.input.c | 236 |
| 6.36 | IP input—find IP—not inline: linux/net/ipv4/ip.input.c | 236 |
| 6.37 | IP input—deliver IP packets 2nd stage: linux/net/ipv4/ip.input.c | 237 |
| 6.38 | IP input—deliver IP packets 1st stage: linux/net/ipv4/ip.input.c | 238 |
| 6.39 | IP input—finish IP reception: linux/net/ipv4/ip.input.c | 238 |
| 6.40 | IP input—finish IP reception: linux/net/ipv4/ip.input.c | 239 |
| 6.41 | IP input—main IP route: linux/net/ipv4/ip.input.c | 240 |
| 6.42 | IP input—main IP route: linux/net/ipv4/ip.input.c | 241 |
| 6.43 | Internet Protocol—forward part: linux/net/ipv4/ip.forward.c | 241 |
| 6.44 | Internet Protocol—forward bit: linux/net/ipv4/ip.forward.c | 242 |
| 6.45 | Internet Protocol—forward bit: linux/net/ipv4/ip.forward.c | 243 |
| 6.46 | Internet Protocol—fragmentation—data: linux/net/ipv4/ip_fragment.c | 244 |
| 6.47 | Fragmentation—hash data: linux/net/ipv4/ip_fragment.c | 245 |
| 6.48 | Fragmentation—memory tracking: linux/net/ipv4/ip_fragment.c | 246 |
| 6.49 | Fragmentation—free up ipq: linux/net/ipv4/ip_fragment.c | 246 |
| 6.50 | Fragmentation—free up space with oldest: linux/net/ipv4/ip_fragment.c | 247 |
| 6.51 | Fragmentation—reassembly timeout, expire a packet: linux/net/ipv4/ip_fragment.c | 248 |
| 6.52 | Fragmentation—create fragment: linux/net/ipv4/ip_fragment.c | 249 |
| 6.53 | Fragmentation—queue whole packet: linux/net/ipv4/ip_fragment.c | 249 |
| 6.54 | Fragmentation—match a fragment to datagram in partial queue: linux/net/ipv4/ip_fragment.c | 250 |
| 6.55 | Fragmentation—add segment to queue: linux/net/ipv4/ip_fragment.c | 251 |
| 6.56 | Fragmentation—add segment to queue: linux/net/ipv4/ip_options.c | 251 |
| 6.57 | Fragmentation—add segment to queue: linux/net/ipv4/ip_fragment.c | 252 |
| 6.58 | Fragmentation—add segment to queue: linux/net/ipv4/ip_fragment.c | 252 |
| 6.59 | Fragmentation—add segment to queue: linux/net/ipv4/ip_fragment.c | 253 |
| 6.60 | Fragmentation—put fragments together: linux/net/ipv4/ip_fragment.c | 254 |
| 6.61 | Fragmentation—put fragments together: linux/net/ipv4/ip_fragment.c | 254 |
| 6.62 | Fragmentation—put fragments together: linux/net/ipv4/ip_fragment.c | 255 |
| 6.63 | Fragmentation—deal with arrival of a fragment: linux/net/ipv4/ip_fragment.c | 256 |
| 6.64 | Internet Protocol—options—build IP option header: linux/net/ipv4/ip_options.c | 257 |
| 6.65 | IP options—echo: linux/net/ipv4/ip_options.c | 258 |
| 6.66 | IP options—echo: linux/net/ipv4/ip_options.c | 258 |
| 6.67 | IP options—echo: linux/net/ipv4/ip_options.c | 259 |
| 6.68 | IP options—echo: linux/net/ipv4/ip_options.c | 260 |
| 6.69 | IP options—zero-out disallowed options in frags: linux/net/ipv4/ip_options.c | 260 |
| 6.70 | IP options—validate inbound packet header options: linux/net/ipv4/ip_options.c | 261 |
| 6.71 | IP options—validate inbound packet header options: linux/net/ipv4/ip_options.c | 262 |
| 6.72 | IP options—validate inbound packet header options: linux/net/ipv4/ip_options.c | 262 |
| 6.73 | IP options—validate inbound packet header options: linux/net/ipv4/ip_options.c | 263 |
| 6.74 | IP options—validate inbound packet header options: linux/net/ipv4/ip_options.c | 264 |
| 6.75 | IP options—validate inbound packet header options: linux/net/ipv4/ip_options.c | 265 |
| 6.76 | IP options—of: linux/net/ipv4/ip_options.c | 266 |
- 6.77 | IP options—of: linux/net/ipv4/ip_options.c | 266 |
- 6.78 | IP options—of: linux/net/ipv4/ip_options.c | 267 |
- 6.79 | IP options—of: linux/net/ipv4/ip_options.c | 268 |
- 6.80 | IP options—receive: linux/net/ipv4/ip_options.c | 269 |
- 6.81 | IP options—receive: linux/net/ipv4/ip_options.c | 269 |
- 6.82 | Internet Protocol—sparse: linux/net/ipv4/ip_fragment.c | 270 |
- 6.83 | Internet Protocol—some: linux/net/ipv4/ip_fragment.c | 270 |
- 6.84 | Internet Protocol—some: linux/net/ipv4/ip_fragment.c | 270 |
- 6.85 | IP socket—field: linux/net/ipv4/ip_fragment.c | 271 |
- 6.86 | IP socket—send: linux/net/ipv4/ip_fragment.c | 272 |
- 6.87 | IP socket—route user: linux/net/ipv4/ip_fragment.c | 273 |
- 6.88 | IP socket—route user: linux/net/ipv4/ip_fragment.c | 273 |
- 6.89 | IP socket—icmp error: linux/net/ipv4/ip_fragment.c | 274 |
- 6.90 | IP socket—local error: linux/net/ipv4/ip_fragment.c | 274 |
- 6.91 | IP socket—map reception: linux/net/ipv4/ip_fragment.c | 275 |
- 6.92 | IP socket—setsockopt: linux/net/ipv4/ip_fragment.c | 276 |
- 6.93 | IP socket—setsockopt: linux/net/ipv4/ip_fragment.c | 277 |
- 6.94 | IP socket—setsockopt: linux/net/ipv4/ip_fragment.c | 278 |
- 6.95 | IP socket—setsockopt: linux/net/ipv4/ip_fragment.c | 279 |
- 6.96 | IP socket—setsockopt: linux/net/ipv4/ip_fragment.c | 280 |
- 6.97 | IP socket—setsockopt: linux/net/ipv4/ip_fragment.c | 281 |
- 6.98 | IP socket—setsockopt: linux/net/ipv4/ip_fragment.c | 282 |
- 6.99 | IP socket—setsockopt: linux/net/ipv4/ip_fragment.c | 283 |
- 6.100 | IP socket—getsockopt: linux/net/ipv4/ip_fragment.c | 284 |
- 6.101 | IP socket—getsockopt: linux/net/ipv4/ip_fragment.c | 285 |
- 6.102 | IP socket—getsockopt: linux/net/ipv4/ip_fragment.c | 286 |
- 6.103 | IP socket—getsockopt: linux/net/ipv4/ip_fragment.c | 287 |
- 6.104 | IP socket—getsockopt: linux/net/ipv4/ip_fragment.c | 288 |
- 6.105 | IP socket—getsockopt: linux/net/ipv4/ip_fragment.c | 289 |
- 6.106 | ARP—data: linux/net/ipv4/arp.c | 290 |
- 6.107 | ARP neighbor operations: linux/net/ipv4/arp.c | 291
