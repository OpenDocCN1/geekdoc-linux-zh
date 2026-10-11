+   - Finding latest version of hashicorp/aws...
+   - Installing hashicorp/aws v4.41.0...
+   - Installed hashicorp/aws v4.41.0 (signed by HashiCorp)

Terraform has created a lock file `.terraform.lock.hcl` to record the provider selections it made previously. Include this file in your version control repository so that Terraform can guarantee to make the same selections by default when you run “terraform init” in the future.

Terraform has been successfully initialized!

You may now begin working with Terraform. Try running the “terraform plan” to see any changes that are required for your infrastructure. All Terraform commands should now work.

If you ever set or change modules or backend configuration for Terraform, rerun this command to reinitialize your working directory. If you forget, other commands will detect it and remind you to do so if necessary.

After the initialization of the directory where the definition is located, the next optional step is to execute the **terraform plan** to check the syntax and the dependencies and show the tasks which will be performed. The following output shows an example:

```
data.aws_vpc.iac-vpc: Reading...
data.aws_ami.ubuntu: Reading...
data.aws_vpc.iac-vpc: Still reading... [10s elapsed]
data.aws_ami.ubuntu: Still reading... [10s elapsed]
data.aws_ami.ubuntu: Read complete after 11s [id=ami-0a3e4ec6adf694c3f]
data.aws_vpc.iac-vpc: Still reading... [20s elapsed]
data.aws_vpc.iac-vpc: Read complete after 23s [id=vpc-065e086222c706994]
data.aws_security_group.allow_http: Reading...
data.aws_subnet.iac-subnet: Reading...
data.aws_subnet.iac-subnet: Read complete after 0s [id=subnet-0faf005c6d517ae9b]
data.aws_security_group.allow_http: Read complete after 0s [id=sg-04313711a4beec2f7]
```