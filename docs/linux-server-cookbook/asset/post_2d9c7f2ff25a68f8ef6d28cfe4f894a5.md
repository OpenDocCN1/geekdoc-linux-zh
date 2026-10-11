
## Automation with Ansible

Ansible is the most popular tool for automation due to the ease of use and the lack of need to install agents in the systems managed. Ansible is able to manage not only operating systems but applications, network devices, infrastructures, and much more. Some of the advantages of this solution are as follows:

- Support for most of the Linux distributions.
- Able to manage Windows systems.
- Simple to learn and use.
- Does not require any agent on the managed devices.
    - This leads to greater security because it is not needed to manage the agent versions or server services.
    - It uses a common protocol such as Secure Sockets Shell (SSH) or WinRM (for Windows nodes), not requiring opening extra ports, and with the possibility to use standard authentication methods.
- A big number of companies collaborating in the project and creating content to manage different systems.

Working with Ansible requires you to know some terminology. Table 12.3 introduces some of the important terms and provides a description:

| Term | Description |
|---|---|
| Playbook | List of Plays to perform in the nodes indicated. |
| Play | List of Tasks to perform in the specified nodes in the Playbook. |
| Inventory | List, static or dynamic, of the nodes to administrate and the information required for each of them (remote IP, username, password, and so on) |
| Host | A remote machine to manage it. It can be a Linux system, a Windows system, or a network device, among multiple options available. |
| Task | A definition of an Action to perform. |
| Action | The action to be performed in a Host |
| Module | Unit of work that Ansible ships out to remote machines. These modules are usually written in Python language. |
| Arguments | Values needed for the Module. |
| Template | A dynamic file is usually used for configuration files, where variables will be evaluated. |
| Facts | Data discovered about remote Hosts. |
| Variable | Values specified statically or dynamically to be used in Playbooks and Templates. |
| Roles | A group of tasks, files, and templates that can be reused in different projects. |
| Collections | A new packaging format for bundling and distributing Ansible content, including roles, modules, and more. |
| Conditions | Check to be performed to know if a Task needs to be performed. |

Table 12.3: Ansible Glossary

Ansible is not installed by default on Linux distributions. As described previously, Ansible does not use agents or a service; the only installation required is the tool in a Linux system which will be used as a control node. The only requirement is to have version Python 3.8 or newer for the latest Ansible versions. This control node which has the Ansible tools installed requires to have communication to the nodes managed or to the jump hosts used to perform the intermediate connection.

It is possible to install Ansible using the Linux distribution’s package manager or using Python’s package manager (pip). The following instructions are used for the installation in an Ubuntu system:

```bash
apt-add-repository ppa:ansible/ansible
apt install -y ansible-core ansible
```

After installation Ansible is able to run the command ansible with the option --version to display the version installed, as shown in the following figure 12.13:

```text
agonzalez@ubuntu:~$ ansible --version
ansible [core 2.13.5rc1]
  config file = /etc/ansible/ansible.cfg
  configured module search path = ['/home/agonzalez/.ansible/plugins/modules', '/usr/share/ansible/plugins/modules']
  ansible python module location = /usr/lib/python3/dist-packages/ansible
  ansible collection location = /home/agonzalez/.ansible/collections:/usr/share/ansible/collections
  executable location = /usr/bin/ansible
  python version = 3.10.4 (main, Jun 29 2022, 12:14:53) [GCC 11.2.0]
  jinja version = 3.0.3
  libyaml = True
```

*Figure 12.13: Ansible version display example*

## Inventory

Ansible can administrate multiple nodes, but for that, it is needed to define an Inventory. This Inventory will contain the list of the hosts to be managed with the different options needed to connect to the system and other configurations required for the automation. Dynamic inventories use Ansible plugins, and that will be covered in Chapter 15, Multi-Cloud Management. Figure 12.14 features an Ansible diagram:

![](img/863afa537de4eed7deb11978bfbfa90e_393_0.png)

> Figure 12.14: Ansible diagram. Source: Ansible website.

The default file containing the list of the hosts to be managed is `/etc/ansible/hosts`. An inventory can group hosts into group hosts. It is also possible to configure variables to groups, which will be applied to all the hosts defined inside. The format of the inventory files can be INItialization (INI) or YAML Ain't Markup Language (YAML).

The following code shows an example of one Inventory with INI format, which is the default used, defining two groups called webservers and observers, and having four servers in each group.

```ini
[webservers]
alpha.example.org
beta.example.org
192.168.1.100
192.168.1.110
[dbservers]
db01.intranet.mydomain.net
db02.intranet.mydomain.net
10.25.1.56
10.25.1.57
```

As observed in the previous example, an inventory can contain a DNS-resolvable name or an IP. Groups can define systems with certain affinities, such as:

- **Geographically**: For example, hosts located in the same data center, city, or country.
- **Application**: Servers running similar applications, such as webs, databases, backup, and so on.
- **Operating system or distribution**: For example, to separate Linux and Windows systems, Ubuntu, and Red Hat Enterprise Linux systems.
- **Environment**: Such as development, test, production, and so on.

A host can be part of several groups, such as being part of development and webservers group. A host can have associated different parameters related to the connection or variables being used during the automation. Refer to the following example:

```ini
[linux]
rhel ansible_host=192.168.122.226 ansible_password=Start123
ubuntu ansible_host=192.168.122.43 ansible_password=Start123
```

The previous example defines two hosts, **rhel**, and **ubuntu**, and the IP and password configuration to connect to the nodes. The DNS, in this case, does not need to be resolved; they are treated as an alias by *Ansible*. The previous example can be rewritten, defining the common variables at the group level instead at the host level as follows:

```ini
[linux]
 rhel ansible_host=192.168.122.43
 ubuntu ansible_host=192.168.122.226
 [linux:vars]
 ansible_user=agonzalez
 ansible_password=Start123
 owner=Alberto
```

In the previous example, a new variable to define the user to be used during the connection is defined: **ansible_user**. Another variable, **owner**, which is not used to define the connection, can be used by tasks or templates during the automation. Some popular variables are listed in table 12.4:

| Variable | Description |
| :--- | :--- |
| *ansible_host* | Defines the *DNS or IP* to connect. |
| *ansible_port* | Defines the port to be used for the connection. |
| *ansible_password* | Not recommended to set it as plain text for security reasons; it defines the password to be used for the connection. Recommended is to use a private/public key or an encrypted value (*vault*). |
| *ansible_user* | Defines the user to be used for the connection. |
| *ansible_connection* | Specifies the connection to be used, for example: `ssh`, `local`, `winrm` |
| *ansible_become* | Indicates to force privilege escalation. |
| *ansible_become_method* | Sets the privilege escalation method, for example: `su`, `sudo` |
| *ansible_become_user* | Sets the user to become through privilege escalation. |
| *ansible_ssh_private_key_file* | Specifies the private key to be used for SSH connection. |
| *ansible_ssh_common_args* | Specifies the arguments to be used for SSH. |

Table 12.4: Ansible variables on the inventory

Ansible auto generates two groups automatically:

- **all**: It includes all the hosts defined in the inventory.
- **ungrouped**: It includes all the hosts which do not belong to any group.

It is also possible to define groups containing another group, as is shown in the following example:

```ini
[production]
anoherost ansible_host=192.168.122.44
[production:children]
linux
windows
[linux]
rhel ansible_host=192.168.122.43
ubuntu ansible_host=192.168.122.226
[windows]
win01 ansible_host=192.168.122.33 ansible_connection=winrm
```

In the previous example, the group production will contain three hosts: rhel, ubuntu, and win01. The node anotherhost will be part of the groups ungrouped and all. Ansible provides a command named ansible-inventory to query the inventory indicated to display the configured inventory. Figure 12.15 shows an example with the option --graph:

```text
agonzalez@ubuntu:~$ ansible-inventory -i /etc/ansible/hosts --graph
@all:
|--@production:
|  |--@linux:
|  |   |--rhel
|  |   |--ubuntu
|  |--@windows:
|     |--win01
|--@ungrouped:
|  |--anotherhost
```

Figure 12.15: Output example for command ansible-inventory
