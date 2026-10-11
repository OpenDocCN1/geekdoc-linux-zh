```
|---/inventory/production/host_vars/ubuntu.yml
| -/inventory/production/group_vars/
|---/inventory/production/group_vars/all.yml
|---/inventory/production/group_vars/linux.yml
|---/inventory/production/group_vars/windows.yml
```

Separating the variables in different files requires the definition to be in *YAML* format. The following code shows an example for the `windows.yml` file:

```
ansible_host: 192.168.122.33
ansible_connection: winrm
```

As described before, an inventory can be in *YAML* format. The previous Inventory defined on *INI* format can be defined as *YAML* as the following:

```
all:
  hosts:
    anotherhost:
      ansible_host: 192.168.122.44
children:
  production:
    children:
linux:
  hosts:
    rhel:
      ansible_host: 192.168.122.43
      ansible_password: Start123
      ansible_user: agonzalez
      owner: Alberto
ubuntu:
  ansible_host: 192.168.122.226
  ansible_password: Start123
  ansible_user: agonzalez
  owner: Alberto
windows:
  hosts:
    win01:
```