```
Port patch-tun
Interface patch-tun
  type: patch
  options: {peer=patch-int}
Port 'tab035/7edc-72'
  tag: 1
Interface 'tab035/7edc-72'
  type: internal
Port 'qr-584feae2-79'
  tag: 1
Interface 'qr-584feae2-79'
  type: internal
Bridge br-tun
fail_mode: secure
Port patch-int
Interface patch-int
  type: patch
  options: {peer=patch-tun}
Port 'vxlam-c0a8*abf'
Interface 'vxlam-c0a8*abf'
  type: vxlan
  options: {df_default=true*, in_key=flow, local_ip='192.168.122.9*', out_key=flow, remote_ip='192.168.122.191*'}
Port br-tun
Interface br-tun
  type: internal
Bridge br-ex
Port phy-br-ex
Interface phy-br-ex
  type: patch
  options: {peer=int-br-ex}
Port 'qq-576e34l8-87'
Interface 'qq-576e34l8-87'
  type: internal
Port br-ex
Interface br-ex
  type: internal
Port 'eth1'
Interface 'eth1'
  ovs_version: '2.5.0'
```

Sometimes OVS isn't properly running after it is either freshly installed or the node is rebooted. This is a known bug with OVS. Restarting the OVS service resolves it, though you wouldn't want to do this in production without planning.

```
$ sudo service openvswitch-switch restart
```

Now you will want to log into the Horizon dashboard, which is opened by using your web browser to navigate to the IP address of your controller. If you're using the reference deployment from Appendix A, accessing the dashboard can be done on your host machine where you run the controller and compute VMs from. Otherwise you'll just need to make sure the machine you run the browser from can access the IP address that the controller is running on.