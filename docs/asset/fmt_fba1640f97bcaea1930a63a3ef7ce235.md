
`表 16.13` 展示了与*卷*相关的常见任务。

| 参数 | 描述 |
| :--- | :--- |

### 编排

如前一章所述，与**公共云**中的*编排*相关，可以在`OpenStack`上编写模板来执行资源创建。编排服务器被称为`Heat`。**以下模板**创建一个新的*虚拟机*并分配一个*浮动 IP*和一个*卷*：

```yaml
heat_template_version: rocky
description: Provision a instance with a floating ip
parameters:
    KeyName:
        description: Name of an existing SSH keypair
        type: string
    InstanceName:
        description: Name of the instance
        type: string
    FlavorSize:
        description: The flavor required for the instance
        type: string
        default: "m1.small"
    ImageName:
        description: The name of an image to deploy
        type: string
        default: "debian10"
    PrivateNet:
        type: string
        description: Private Network
    ExternalNet:
        type: string
        description: External Network
    SecurityGroup:
        type: string
        description: Security group
        default: "default"
    VolumeSize:
        type: number
        description: Size of the volume to be created.
        default: 1
resources:
    instance:
        type: OS::Nova::Server
        properties:
            flavor: { get_param: FlavorSize }
            image: { get_param: ImageName }
            key_name: { get_param: KeyName }
            name: { get_param: InstanceName }
            networks:
                - port: { get_resource: instance_port }
    instance_port:
        type: OS::Neutron::Port
        properties:
            network: { get_param: PrivateNet }
            security_groups:
                - { get_param: SecurityGroup }
    instance_external:
        type: OS::Neutron::FloatingIP
        properties:
            floating_network: { get_param: ExternalNet }
            port_id: { get_resource: instance_port }
    volume:
        type: OS::Cinder::Volume
        properties:
            size: { get_param: VolumeSize }
            name: dataVolume
            description: Cinder Volume Test
    instance_volume:
        type: OS::Cinder::VolumeAttachment
        properties:
            instance_uuid: { get_resource: instance }
            volume_id: { get_resource: volume }
            mount_point: /dev/vdb
outputs:
    instance_external_ip:
        description: Floating IP address of instance in External network
        value: { get_attr: [ instance_external, floating_ip_address ] }
```

使用`stack create`来处理模板并创建资源。选项`--parameter (-p)`用于以`key=value`格式传递参数。下图 16.26 展示了使用上一模板创建虚拟机的示例：
