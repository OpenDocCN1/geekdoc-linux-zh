
<ansible> `SSH -vv -o ControlMaster=auto -o ControlPersist=60 -o StrictHostKeyChecking=no -o AuthenticationMethods= -o PreferredAuthentications=ssh,publickey -A /ansible@ansible"`

<ansible> `SSH -vv -o ControlMaster=auto -o ControlPersist=60 -o StrictHostKeyChecking=no -o AuthenticationMethods= -o PreferredAuthentications=ssh,publickey -A /ansible@ansible"`

...

<ansible> `SSH -vv -o ControlMaster=auto -o ControlPersist=60 -o StrictHostKeyChecking=no -o AuthenticationMethods= -o PreferredAuthentications=ssh,publickey -A /ansible@ansible"`

```


### 考试提示

在目前为止你看到的故障排除选项中，输出详细程度（output verbosity）选项并不是最有用的。运用常识更为有效。playbook（剧本）中的大多数错误是逻辑错误导致的，即 playbook 中的任务流没有经过周全考虑。避免这类错误相对容易：不要在一个 play（副本）中包含过多的任务，也不要在 playbook 中包含过多的 play。这样，你就能很容易避免失去控制。

### 练习 5-3 你将编写一个多 play 的 playbook。

## 练习 5-3 创建多 play 的 playbook

- 1. 使用编辑器创建`exercise53.yaml`文件并创建第一个 play：

```yaml
---

- name: enable web server

  hosts: ansible1

tasks:

  - name: install stuff

    yum:

      - httpd

      - firewalld

  - name: create a welcome message

    copy:

      content: "welcome to the webserver\n"

      dest: /var/www/html/index.html

  - name: enable webserver

    service:

      name: httpd

      state: started

      enabled: true
```

```yaml
- name: enable firewall

  service:

    name: firewall

    state: started

    enabled: true

- name: open service in firewall firewalld:

  service: http

    permanent: true

    state: enabled

    immediate: yes
```
