shut down and then restarted at will, on the same instance type or on another one with different specifications; however, you can't migrate between instance types with different word sizes without rebuilding the AMI.

Each of your EC2 instances can be included in any number of EC2 security groups when the instance is launched. The security groups are part of your AWS account and can be applied to any number of instances. Each group defines a set of allowable inbound connections using rules that contain a protocol, a port, and an IP address range. Once an instance is launched, the set of groups attached to it cannot be changed. However, the group itself can be changed (rules added or deleted) and the changes will take effect immediately. Groups can be used to implement fine-grained access control logic for multi-tier applications. For instance, Table 5.2 describes one way to set up your security groups.

# Table 5.2. Sample Security Groups

Group Name | Rules
:----------------------:|:-----------------------------------------:
web_access | □ allow HTTP access (port 80) from anywhere
 | □ allow SSH access (port 22) from corporate network
db_access | □ allow access to MySQL database (port 3306)
 | □ allow SSH access (port 22) from corporate network
app_access | □ allow access to application server (port 5000)
 | □ allow SSH access (port 22) from corporate network

The security groups would then be applied to the instances as listed in Table 5.3.

# Table 5.3. Instances and Security Groups

Instance Role | Security Group
:----------------------:|:----------------------:
web server | web_access
database server | db_access
application server | app_access

With a clean and properly factored set of groups as a base, it becomes possible to think about making changes dynamically. For example, a scheduling utility built