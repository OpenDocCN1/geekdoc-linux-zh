Define the problem. Be able to clearly state the problem and its symptoms. Be as specific as possible. Detail the steps which will reproduce the problem.

Gather background information. Which product and version is affected? Be ready to provide relevant information. This can include output of sosreport, discussed in this section. For kernels, this could include the system's kdump crash dump or digital photo of the kernel backtrace displayed on the monitor of a crashed system.

Determine the severity level. Red Hat has four severity levels to classify issues. Urgent and High severity problems should be followed by a phone call to the relevant local support center (see https://access.redhat.com/site/contact/technicalSupport).

| SEVERITY | DESCRIPTION |
| Urgent (Severity 1) | A problem that severely impacts your use of the software in a production environment. This includes loss of production data or malfunctioning production systems. The system halts your business operations and no procedural workaround exists. |\| High (Severity 2) | A problem where the software is functioning but in a production environment is severely reduced. The situation is causing a high impact to your business operations and no procedural workaround exists. |\| Medium (Severity 3) | A problem that involves partial, not critical use of software in a production environment or development environment. For production environments, there is a medium to low impact on your business. Business continues to function using a procedural workaround. For development environments, the situation is causing problems migrating your project into production. |\| Low (Severity 4) | A general usage question, reporting of a documentation error, or recommendation for a future product enhancement or modification. For production environments, there is low to no impact on your business or the performance or functionality of your system. For development environments, there is a medium to low impact on your business, but your business continues to function using a procedural workaround |

# # Managing A Bug Report with redhat-support-tool

Subscribers may create, view, modify, and close Red Support cases using redhat-support-tool. When cases are in an open or maintained status, users may attach files or documentation, such as diagnostic reports (sosreport). The tool uploads and attaches files to cases.

Case details including product, version, summary, description, severity, and case group may be assigned with command options or letting the tool prompt for required information. In the following example, a new case is opened. The --product and --version options are specified.

```
[user@]$ redhat-support-tool.
Welcome to Red Hat Support Tool.
Command (? for help): opencase --product="Red Hat Enterprise Linux" --nversion="7.0"
Please enter a summary (or 'q' to exit): System fails to run without power
nPlease enter a description (Ctrl-D on an empty line when complete):
```