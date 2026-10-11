# Secure access to your AWS resources

Protect your web platform from online attack to keep data safe and your service operational

![](bbox=[0.07, 0.27, 0.19, 0.36])

![](bbox=[0.07, 0.37, 0.19, 0.47])

Philipe Martins & Anna Kobylinska
earned up to decades ago on a Linux box and ended up in enterprise IT, designing cloud topologies, optimising Linux VMs and managing AWS deployments.

Those who dare to venture into the public cloud quickly learn the value of paranoid security. In the cloud, you are no longer 'merely' facing the risk of a catastrophic data loss or data leak. You are now looking at what amounts to an unlimited financial liability for your pay-as-you-go services that scale on demand. Should an unauthorised party gain control over your AWS account, the financial outcome wouldn't look pretty. Not even close. It is wise to never understate human ingenuity, because the impossible may not be so far-fetched after all.

Over the last year or so, a series of security vulnerabilities, from Heartbleed through Shellshock to VENOM, struck terror into the hearts of active cloud users around the world. Heartbleed and Shellshock famously exposed fatal flaws in tools that were previously deemed to be safe (OpenSSL and Bash, respectively). VENOM forced hurried patching from esteemed vendors of virtualisation software, having lurked in obscurity for over a decade.

When it comes to cloud security, Andy Grove's (former CEO of Intel) remark "only the paranoid survive" seems fitting. On AWS, security is a feature you don't have to pay extra for.

+   01 Create a new IAM user
+   In order to secure access to your AWS resources, you need to quit using your AWS root credentials. The AWS Management Console, Amazon's web frontend for its infrastructure services, may prompt you to create an IAM user. Even if it doesn't, you should still do so.
+   
+   Navigate your web browser to the service Identity and Access Management (IAM for short), which is located at: console.aws.amazon.com/iam. In the left-hand navigation pane, switch to the section labeled Users and click on the button Create New Users.
+   
+   Follow the on-screen instructions in the IAM dashboard to create new users. The wizard will ask you to provide up to five usernames with a maximum of 64 characters each. An access key is optional; if you deactivate the checkbox, you can still add these credentials later.
+   
+   Once you click on the Create button, up to five IAM users will be added to your AWS root account. So far, these users do not belong to any groups and they have no privileges whatsoever. The real users also do not yet know their login credentials and so do not have access.

# Resources

AWS root account

![](bbox=[0.19, 0.62, 0.95, 0.9])

**Right:** Through the Identity and Access Management Console, create new IAM users