```
```
+ "Name" = "web01"
  }
+ tags_all                                = {
+ "Name" = "web01"
  }
<<OMITTED>>
  }
Plan: 1 to add, 0 to change, 0 to destroy.
Changes to Outputs:
  + instance_ip_addr = (known after apply)
```
```

> **Note: You did not use the -out option to save this plan, so Terraform cannot guarantee to take exactly these actions if you run “terraform apply” now.**

If no errors were found in the definition provided, it is possible to execute **terraform apply** to the provision of the definition to the target environment. The following output shows the example output for the previous example:

```
```
<<OMITTED>>
Do you want to perform these actions?
  Terraform will perform the actions described above.
  Only 'yes' will be accepted to approve.
Enter a value: yes
aws_instance.web01: Creating...
aws_instance.web01: Still creating... [10s elapsed]
aws_instance.web01: Still creating... [20s elapsed]
aws_instance.web01: Creation complete after 28s [id=i-
0c5d6e9700ea03a06]
Apply complete! Resources: 1 added, 0 changed, 0 destroyed.
Outputs:
  instance_ip_addr = "18.159.48.0"
```
```

*Figure 15.6* shows the output connecting to port 80 of the external IP shown in the previous example: