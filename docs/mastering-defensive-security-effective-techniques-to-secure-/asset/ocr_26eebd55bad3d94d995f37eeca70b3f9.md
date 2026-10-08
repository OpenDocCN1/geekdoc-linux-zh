Additionally, we are going to go over some best practices to harden your cloud databases and also discuss the best systems to monitor your cloud infrastructure.

Here are the main topics that we will cover in this chapter:

+   - Secure deployment and implementation of cloud applications
- Securing Kubernetes and APIs
- Hardening database services
- Testing your cloud security

# Technical requirements

There are no technical requirements for this chapter, however, you can create free accounts to test some of the tools that we will review. Also, most of the cloud services offer free trials (tiers) that you can leverage to put the concepts into practice.

# Secure deployment and implementation of cloud applications

Almost all companies have a least portion of their business on the cloud. However, each company is unique, and their implementation of cloud services could be a blend of the different cloud models available, as explained next.

# Security by cloud models

There are three types of cloud models: **Software as a Service (SaaS), Platform as a Service (PaaS), and Infrastructure as a Service (IaaS)**. Each of these models is very different from the others and therefore the security measurements that need to be applied for each of them. Therefore, let's start by giving a quick introduction to the three types of cloud environments to better understand what we are aiming to protect.

# Software as a Service (SaaS)

This is basically a piece of software loaded on the cloud that can be easily accessed by the user through a web interface. Some examples are the following:

+   - Web-based emails such as **Gmail** and **Outlook**
- Web tools such as web-based billing systems or ticketing systems
- Web-based productivity applications such as **Office 365** or **Google Workspace**