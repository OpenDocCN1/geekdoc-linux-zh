```
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
```