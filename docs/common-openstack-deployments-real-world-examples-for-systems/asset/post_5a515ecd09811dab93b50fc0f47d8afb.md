
# Index

## Networking Guide
- 49

### Neutron networking
- compute node installation of, 84–85
- compute node setup, 57–58
- configuring first OpenStack, 55–56, 76–83
- controller node setup, 55–56
- deployment requirements, 39–43, 92–93
- DevStack deployment failures, 23
- exploring possibilities with, 96–97
- in Horizon, 6–7
- initial setup, 52–53
- as key component, 9–10
- Magnum containers, 197
- Maximum Transmission Units, 38–39
- other resources, 49
- planes of operations, 35–36
- profile, 103–105
- provider networks, 36
- selecting for deployment, 96
- significance of, 35
- tenant networks, 36–38
- traffic flow, 43–44
- traffic flow on compute mode, 48–49
- troubleshooting, 217–221
- troubleshooting as key service, 216–217

### Neutron-server
- Neutron, 10

### NICs
- reference deployment, 231–233
- simple deployment requirements, 51–52
- virtual machine deployment setup, 42

### Nodes
- classification of Puppet, 238
- cleaning Ironic, 192
- definition of, 42
- Magnum, 198–199
- networking deployment, 39–43

### Nova-api daemon
- defined, 8
- deploying Nova in controller node, 97
- screen session for DevStack, 30–33

### Nova-api-metadata daemon
- 8, 97

### Nova compute
- container drivers, 197
- DevStack deployment as user, 25
- installing in compute mode, 83–84
- installing on controller, 72–75
- as key component, 7–9
- profile, 103
- restarting all services, 81
- selecting for deployment, 97
- viewing statistics with dashboard, 146–147

### Nova-compute daemon
- 7–8, 83, 97

### Nova-conductor daemon
- 7, 97

### Nova-connelauth daemon
- 8

### Nova-novncproxy daemon
- 8

### Nova-scheduler daemon
- 7, 97

### Nova-spicehtml5proxy daemon
- 8

### Nova-vxvpproxy daemon
- 8

### Novncproxy daemon
- 73

### NTP (Network Time Protocol)
- base profile setup, 100
- ntp daemon, 56, 58

## O

### Object daemon
- Swift, 170

### Object storage
- See *Swift object storage*

### Object Store
- Swift
    - backing up block data to, 153
    - creating container/object in dashboard, 176–178
    - using objects, 181–184

### Objects
- Swift
    - adding to container in dashboard, 176–179
    - adding to container in OSC, 179–181
    - connecting to Swift, 171–172
    - getting details about, 177, 179–181
    - overview of, 171
    - using, 181–184

### Online gaming company
- using containers, 196

### Open source
- OpenStack commitment to, 3
- Puppet modules deploying OpenStack, 99–100
- vendor-specific drivers/agent plug-ins for Neutron, 96–97

### Open vSwitch
- See OVS (Open vSwitch)

### Openrc credentials
- testing compute node, 111

### Openrc files
- base profile, 100

### OpenSSH
- reference deployment, 231

### Openssh-server package
- reference deployment, 233

### OpenStack
- building cloud, 3
- cloud, 1–2
- OpenStack joins the cloud, 2–3
- release cycle, 13–16
- summary review, 17
- understanding, 1
- uses, 3–4

### OpenStack Administrator Guide
- 208

### OpenStack Ansible Deployment (OSAD)
- 93

### OpenStack Client
- See OSC (OpenStack Client)

### OpenStack Continuous Integration
- launching DevStack, 31–32

### OpenStack Design Summit and Conference
- 3, 243–244

### openstack-dev mailing list
- 244

### openstack endpoint: create command
- 250

### OpenStack Foundation
- creation of, 2
- mailing lists, 254

### Marketplace
- See OpenStack Marketplace

### OpenStack Summit
- 3, 255

### OpenStack Infrastructure team
- hybrid cloud, 228–229

### OpenStack Infrastructure User Manual
- 247

### OpenStack, key components
- baremetal (Ironic), 12
- block storage (Cinder), 10–11
- compute (Keystone), 9
- compute (Nova), 7–9
- containers (Magnum), 13
- dashboard (Horizon), 4–7
- image service (Glance), 10
- instances, 4
- networking (Neutron), 9–10
- object storage (Swift), 11–12
- orchestration (Heat), 12–13
- other projects, 13
- Queuing, 4
- telemetry (Ceilometer), 11–12

### OpenStack Kilo release cycle
- 2015, 13

### OpenStack Marketplace
- finding drivers at, 97, 154
- finding help at, 256
- finding vendors at, 226, 236, 256
- public cloud companies, 141

### openstack network list command
- Ironic, 191

### Openstack-operators mailing list
- 244

### OpenStack project
- hybrid cloud deployments, 228–229

### openstack server create command
- Ironic, 191

### openstack server list command
- testing compute node, 112

### openstack server show fernet command
- 112, 135

### OpenStack Technical Committee (TC)
- 13, 209, 243

### openstack token issue command
- 250

### OpenStack-Trove
- 186

### Openstack-user mailing list
- 244

### Openstackllob module
- 101

### Operating system
- DevStack requirements, 22
- initial network setup of, 54

### Ops Mectops
- finding OpenStack help, 255

### Orchestration
- See Heat orchestration

### Organizations
- cost of public cloud and, 227
- private compute cloud use across, 117–118

### OSAD (OpenStack Ansible Deployment)
- 93

### OSC (OpenStack Client)
- authentication, 249–250
- base profile setup, 100–101
- commands, 250
- creating/attaching volume, 161–163
- creating container/object in Swift, 179–181
- exploring whole cloud deployment, 207
- installing on controller, 67
- interactive mode, 250–251
- launching instance, 128–130
- overview of, 249
- quick reference for commands, 251
- troubleshooting reading displayed errors, 213
- using objects, 182
- viewing statistics on public cloud, 147–149

### Oslo
- 74–75, 78–79

### OVS (Open vSwitch)
- concept of bridge in, 46
- configuring controller node, 56
- installing Neutron in compute mode, 85
- installing Neutron on controller, 78–80
- network deployment, 40–43
- restarting in development environment, 229
- segmented networks using, 37
- testing in controller node, 107–108
- traffic flow on controller node, 45–48
- troubleshooting bridges with, 220
- in tunnel-driven networks, 38–40
- ovs-vsctl, command, 220

## P

### PaaS (Platform as a Service)
- 2

### Packages
- configuring compute node, 58
- configuring controller node, 56
- configuring Keystone, 59
- installing Neutron, 77
- installing Nova, 73–74
- Puppet, 239, 240
- reference deployment, 231

### Partition table
- creating volume in dashboard, 158

### Partitions
- Swift vs. standard disk, 171
- used by Rings in Swift, 170–171

### Passwords
- controller node, 56, 98
- DevStack deployment, 23, 28–29
- Glance, 68–71
- Hiera, 238
- Horizon dashboard user login, 25
- installing Neutron, 76, 78, 80
- installing Nova, 72–75, 83
- Keystone, 64–66
- managing instances, 87

### patch-iptables
- 46

### patch-tun patch
- testing OVS in controller node, 107–108
- traffic flow in compute node, 48–49
- traffic flow on controller node, 45–46

### Patches
- definition of, 46
- testing OVS in controller node, 107–108
- traffic flow in compute node, 48–49
- traffic flow on controller node, 45, 47–48

### Periodic processes
- Swift, 11

### Permissions
- DevStack deployment failures, 23

### Pets vs. cattle metaphor
- cloud computing, 152

### Physical hardware
- creating first OpenStack, 51
- deployment requirements, 40–41, 91–92

### Physical network
- initial setup, 52

### Ping test
- logging in with SSH, 136–137
- on network namespacing, 218

### Pixie Boots
- Ironic mascot, 192

### Planes of operations
- networking, 35–36

### Platform as a Service (PaaS)
- 2

### Plug-ins
- Cinder, 11
- installing Neutron, 80, 84–85
- Neutron, 10, 77, 96–97

### Preboot Execution Environment (PXE)
- Ironic, 12, 186–187

### Private compute cloud
- deployment scenario, 119
- hybrid cloud deployments using, 228–229
- launching instance with dashboard, 119–130
- launching instance with OpenStack Client, 130–136
- overview of, 117
- requirements, 118
- running service, 136–138
- SDKs and OpenStack APIs, 138
- selecting components, 119
- uses, 117–118

### Production machines
- avoid running DevStack on, 21

### Profiles
- base profile, 100–101
- Ceilometer, 144
- Cinder block storage, 156
- Glance imaging service, 101
- Horizon dashboard, 102
- Keystone identity, 102–103
- Neutron networking, 103–105
- Nova compute, 103
- Puppet, 99–100, 239
- RabbitMQ queuing, 105

### Project Navigator
- OpenStack website, 209
