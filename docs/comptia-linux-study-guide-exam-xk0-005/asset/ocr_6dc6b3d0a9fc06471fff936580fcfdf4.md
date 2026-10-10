# Provisioning the Data Center

When implemented correctly, container orchestration provides a way to increase the speed and agility of application deployment. Whether your company's data center is local or in the cloud, you can use orchestration concepts to quickly set up your app's required infrastructure. A few important infrastructure provisioning concepts are covered in the following sections.

# Coding the Infrastructure

Much like a physical data center, a container infrastructure needs to be managed and controlled. In orchestration, the container's configuration is treated in a manner similar to how software revisions are treated:

+   •   **Determine the infrastructure.**   Along with the app requirements, the environment on which the app is executed must be preplanned. This activity is a mutual one between software development and tech ops. In this mutual activity, the container's operating system, libraries, services, security configuration, and any other supporting software or networking utilities are chosen.

The determined infrastructure is frozen to provide a nonchanging (immutable) environment for development and then production. Typically this app container infrastructure is only accessible via the app's or developer's API. Remote access services such as OpenSSH are not provided in order to protect its immutable environment.

+   •   **Document the infrastructure.**   The preset app container infrastructure is typically documented through an orchestration tool. The configuration management and policy as code settings (covered earlier in this chapter) are loaded into the utility's infrastructure as code portal, in a process called *automated configuration management*. The data is later used to deploy and replicate the app containers through *build automation*.

+   •   **Provide revision control.**   The infrastructure as code information is not just documented—it is also inserted into an orchestration code registry, providing version control. Every time a change occurs in the container image infrastructure, its modifications are tracked.

+   •   **Troubleshoot the infrastructure.**   If an app container is deployed into production and problems occur, tech ops, software developers, or both handle the troubleshooting process. One item to check is the production container's documented configuration (as well as its revisions) to determine if any infrastructure items may be to blame.

This provides an easier method for tracking down that pesky new software library that caused all the problems. Various orchestration tools allow a quick determination of modified infrastructure components and quicker problem resolution.