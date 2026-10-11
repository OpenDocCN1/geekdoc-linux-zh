dest: /etc/hosts

# Blocks

Ansible allows to group several tasks in a Block. This allows to specify a different parameter such as become, become_user or user. The expression used to define a Block is block, and it contains a list of tasks. The following code shows a Play example using a block:

```
- name: Block example
  hosts: linux
  become: True
  tasks:
    - name: Install and configure Ubuntu systems
      when: ansible_distribution == "Ubuntu"
      block:
        - name: Install required packages
          ansible.builtin.apt:
            name: "{{ item }}"
          loop:
            - apache2
            - php
            - php-mysql
        - name: Generate index.html file
          ansible.builtin.copy:
            content: "Hello to {{ ansible_hostname }}"
            dest: /var/www/html/index.html
```

# List of popular modules

Ansible brings a big number of the core modules to perform a wide variety of tasks in the managed hosts. The following list shows some of the modules inside the ansible.builtin collection:

+   - add_host: Add a host (and alternatively a group) to the ansible-playbook in-memory inventory.
+   - apt: Manages apt-packages.