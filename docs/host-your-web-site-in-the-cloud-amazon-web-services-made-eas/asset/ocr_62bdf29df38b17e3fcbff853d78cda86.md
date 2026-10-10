# Table 9.1. Amazon RDS DB Instance Classesᵃ

| Name | CPU Virtual Cores | CPU Core Speed (EC2 Compute Units) | RAM | Cost/Hour |
| :--- | :--- | :--- | :--- | :--- |
| Small | 1 | 1 | 1.7GB | $0.11 |
| Large | 2 | 2 | 7.5GB | $0.44 |
| Extra Large | 4 | 2 | 15GB | $0.88 |
| Double Extra Large | 4 | 3.25 | 34GB | $1.55 |
| Quadruple Extra Large | 8 | 3.25 | 68GB | $3.10 |

ᵃ As is the case with all prices mentioned in this book, these are subject to change over time.

You can change the class of a DB Instance in a matter of minutes, so avoid spending too much time trying to decide which one you’ll need up-front. The costs in Table 9.1 reflect the cost of the Single-AZ deployment for a DB Instance. For Multi-AZ deployments, the cost for the DB Instance is double that for a Single-AZ deployment.

The DB Instances have no fixed amount of storage. Instead, you specify an initial storage allocation of 5GB to 1,024GB when you create the DB Instance. You can add more space (up to the limit of 1,024GB) as your needs (and data) expand. The amount of space that you specify is known as the **allocated storage** for the DB Instance. Additional storage allocation can be added to your DB Instance on the fly without incurring downtime.

You must specify a **DB Instance identifier** when you create a DB Instance. This is a string that must start with a lower-case letter and can contain up to 63 lower-case letters, digits, and hyphens. The identifier cannot end with a hyphen, nor contain consecutive hyphens. The identifier must be unique within your account.

Each DB Instance hosts a single copy of a particular **database engine**. The only supported engine at press time is version 5.1 of MySQL; the corresponding database engine identifier is `MySQL5.1`.