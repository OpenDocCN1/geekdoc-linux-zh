
```yaml
name: test html page is installed
content: "Welcome to the example.com intranet!\n"
dest: /var/www/html/index.html
```

第一个条目为任务提供了描述性名称。第二个条目缩进六个空格并调用 `copy`。其余条目缩进八个空格，并传递必要的参数以确保网页中包含正确的内容。

## 4. 在剧中定义两个任务，以确保防火墙服务正在运行并在启动时自动启动，并且允许对 httpd 服务的连接

### 4.1 添加行以确保防火墙服务已启用并正在运行。确保第一行缩进四个空格

```yaml
name: firewall enabled and running
service:
  name: firewall
  enabled: true
  state: started
```

第一个条目为任务提供了描述性名称。第二个条目缩进八个空格并调用 `service` 模块。其余条目缩进十个空格，并传递必要的参数以确保防火墙服务已启用并启动。

### 4.2 添加行以确保防火墙允许来自远程系统的 HTTP 连接。确保第一行缩进四个空格

```yaml
name: firewall permits access to httpd
firewall:
  service: http
  permanent: true
  state: enabled
  immediate: yes
```

第一个条目为任务提供了描述性名称。第二个条目缩进六个空格并调用 `firewall` 模块。其余行缩进八个空格，并传递必要的参数以确保远程 HTTP 连接被永久允许。

## 第 3 章 | 实现剧本（Playbooks）

### 5. 在第一个剧中添加一个最后一个任务，确保 httpd 服务正在运行并在启动时自动启动

添加以下行以确保 httpd 服务已启用并正在运行。确保第一行缩进四个空格。

```yaml
- name: httpd enabled and running
  service:
    name: httpd
    enabled: true
    state: started
```

第一个条目为任务提供了描述性名称。第二个条目缩进六个空格并调用 `service` 模块。其余条目缩进八个空格，并传递必要的参数以确保 httpd 服务已启用并运行。

### 6. 在 `/home/student/playbook-multi/intranet.yml` 中，定义一个针对 `localhost` 的第二个剧，将用于测试内网 Web 服务器。它不需要权限提升

#### 6.1. 添加以下行来定义第二个剧的开始。注意这里没有缩进

```yaml
- name: Test intranet web server
```

#### 6.2. 添加以下行以指示该剧适用于 `localhost` 托管主机。确保该行缩进两个空格，表示它包含在第二个剧中

```yaml
hosts: localhost
```

#### 6.3. 添加以下行以禁用权限提升。确保缩进与上面的 `hosts` 关键字对齐

```yaml
become: no
```

#### 6.4. 在 `/home/student/playbook-multi/intranet.yml` 文件中添加以下行来定义任务列表的开始。确保该行缩进两个空格，表示它包含在第二个剧中

```yaml
tasks:
```

### 7. 在第二个剧中添加一个简单任务，并使用 `uri` 模块从 `http://servera.lab.example.com` 请求内容。该任务应验证返回的 HTTP 状态码 200。配置剧将返回的内容在任务结果变量中

添加以下行以创建从控制节点验证服务的任务。确保第一行缩进四个空格。

```yaml
name: connect to intranet web server
uri:
  url: http://servera.lab.example.com
  return_content: yes
  status_code: 200
```

第一行为任务提供了描述性名称。第二行缩进六个空格并调用 `uri` 模块。其余行缩进八个空格，并传递必要的参数以执行从控制节点到托管主机的 Web 内容查询，并验证收到的状态码。`return_content` 关键字确保服务器的响应被添加到任务结果中。

### 8. 验证 `/home/student/playbook-multi/intranet.yml` 剧本是否反映了以下结构化内容，然后保存并关闭文件

```yaml
name: Enable intranet services
hosts: servera.lab.example.com
become: yes
tasks:
  - name: latest version of httpd and firewall installed
    yum:
      - httpd
      - firewall
    state: latest
  - name: test html page is installed
    copy:
      content: "Welcome to the example.com intranet!\n"
      dest: /var/www/html/index.html
  - name: firewall enabled and running
    service:
      name: firewall
      enabled: true
      state: started
  - name: firewall permits access to httpd service
    firewall:
      service: http
      permanent: true
      state: enabled
      immediate: yes
  - name: httpd enabled and running
    service:
      name: httpd
      enabled: true
      state: started

  - name: Test intranet web server
    hosts: localhost
    become: no
    tasks:
      - name: connect to intranet web server
        uri:
          url: http://servera.lab.example.com
          return_content: yes
          status_code: 200
```

### 9. 运行 `ansible-playbook --syntax-check` 命令来验证 `/home/student/playbook-multi/intranet.yml` 剧本的语法

```bash
$student@workstation playbook-multi]$ ansible-playbook --syntax-check
intranet.yml

playbook: intranet.yml
```

### 10. 使用 `-v` 选项执行剧本输出每个任务的详细结果。阅读生成的输出以确保所有任务已完成。验证对 `http://servera.lab.example.com` 的 HTTP 请求提供了正确的内容
