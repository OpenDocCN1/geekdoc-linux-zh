Terraform used the selected providers to generate the following execution plan. Resource actions are indicated with the following symbols:
+ create
Terraform will perform the following actions:
# aws_instance.web01 will be created

```
```
+ resource "aws_instance" "web01" {
  + ami                           = "ami-0a3e4ec6adf694c3f"
  + arn                           = (known after apply)
  + associate_public_ip_address   = true
  + availability_zone             = (known after apply)
  + cpu_core_count                = (known after apply)
  + cpu_threads_per_core          = (known after apply)
  + disable_api_stop              = (known after apply)
  + disable_api_termination       = (known after apply)
  + ebs_optimized                 = (known after apply)
  + get_password_data             = false
  + host_id                       = (known after apply)
  + host_resource_group_arn       = (known after apply)
  + id                            = (known after apply)
  + instance_initiated_shutdown_behavior = (known after apply)
  + instance_state                = (known after apply)
```
```