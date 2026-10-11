```
wget -0- https://apt.releases.hashicorp.com/gpg | gpg --dearmor
| sudo tee /usr/share/keyrings/hashicorp-archive-keyring.gpg
echo "deb [signed-by=/usr/share/keyrings/hashicorp-archive-keyring.gpg] https://apt.releases.hashicorp.com $(lsb_release -cs) main" | sudo tee /etc/apt/sources.list.d/hashicorp.list
sudo apt update && sudo apt install terraform
```

# Running a simple Web server on AWS

The definition on Terraform is plain text files with an ending .tf. For the simplicity of this example, all the definitions are in the same file instead of being distributed in several ones (the recommended way). An existing VPC named iac-vpc is already configured on AWS. The content of the file main.tf is as follows:

```
data "aws_ami" "ubuntu" {
  most_recent = true
  filter {
    name   = "name"
    values = ["ubuntu/images/hvm-ssd/ubuntu-jammy-22.04-amd64-server-*"]
  }
  owners = ["099720109477"] # Canonical
}

data "aws_vpc" "iac-vpc" {
  cidr_block = "10.0.0.0/16"
  tags = {
    Name = "iac-vpc"
  }
}

data "aws_subnet" "iac-subnet" {
  vpc_id     = data.aws_vpc.iac-vpc.id
  cidr_block = "10.0.0.0/20"
}

data "aws_security_group" "allow_http" {
  vpc_id     = data.aws_vpc.iac-vpc.id
```