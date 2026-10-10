| Field | Value |
| :--- | :--- |
| mtu | 1500 |
| name | ext-net |
| provider:network_type | flat |
| provider:physical_network | br-ex |
| provider:segmentation_id | |
| router:external | True |
| shared | True |
| status | ACTIVE |
| subnets | |
| tags | |
| tenant_id | 716e41286e1b46fe8238508349e94ffd |
| updated_at | 2016–05–17T02:56:07 |

```
$ neutron subnet-create ext-net 203.0.113.0/24 --name ext-subnet \\
--allocation-pool start=203.0.113.5,end=203.0.113.200 --disable-dhcp \\
--gateway 203.0.113.1
```

| Field | Value |
| :--- | :--- |
| allocation_pools | [{"start": "203.0.113.5", "end": "203.0.113.200"}] |
| cidr | 203.0.113.0/24 |
| created_at | 2016-05-17T02:57:39 |
| description | |
| dns_nameservers | |
| enable_dhcp | False |
| gateway_ip | 203.0.113.1 |
| host_routes | |
| id | 0329b04b-2ebf-4ef3-be96-4a0f0f7f1160 |
| ip_version | 4 |
| ipv4_address_mode | |
| ipv6_ra_mode | |
| name | ext-subnet |
| network_id | 3016c117-052d-44e8-8115-ce9290ccd2e6 |
| subnetpool_id | |
| tenant_id | 716e4128e1b46fe8238508349e94ffd |
| updated_at | 2016-05-17T02:57:39 |

```
$ neutron net-create Network1 --provider:network_type vlan --shared
Created a new network:
```

| Field | Value |
| :--- | :--- |
| admin_state_up | True |
| availability_zone_hints | |
| availability_zones | |
| created_at | 2016–05–17T02:58:45 |
| description | |
| id | 94d79735-dd56-4f5f-b49e-13a13b76c7d6c |
| ipv4_address_scope | |
| ipv6_address_scope | |
| mtu | 1450 |
| name | Network1 |
| provider:network_type | vlan |
| provider:physical_network | |
| provider:segmentation_id | 93 |
| router:external | False |
| shared | True |