# Ubuntu 22.04 LTS

![](bbox=[0.06, 0.09, 0.58, 0.32])

**Figure 3:** A local Kubernetes, including a dashboard, can be set up quite quickly thanks to MicroK8s.

itself on Docker Hub, but also numerous validated container images with MySQL, PostgreSQL, and NGINX. New additions include Grafana Loki, Apache Kafka, and Apache Cassandra.

If you are looking to build a larger container environment, you will find Kubernetes v1.23 in Ubuntu 22.04 [8]. While Canonical recommends its Charmed Kubernetes for enterprise deployments, the leaner MicroK8s (Figure 3) instead targets users who want to run the container orchestrator in edge computing or the Internet of Things (IoT) area. And, last but not least, Canonical Kubernetes also enables managed containerization with a managed Kubernetes.

# Development Drive

Developers use Ubuntu because it supports numerous programming languages out of the box. And Windows users now also have an easy option for using familiar Linux tools in Windows Subsystem for Linux (WSL 2), which now also supports Ubuntu 22.04.

Of particular interest to developers, PHP 8.1.2 is included. If you want to move up from version 7.x, note that version 8 removes some deprecated functions. As a result, some code adjustments may be needed. In return, PHP 8 promises better performance. Ruby 3.0 runs up to three times faster than its predecessor thanks to the MJIT compiler, concurrency, and static types, which is likely to go down well with its followers.

Python fans can look forward to version 3.10.4 and the Python-based Django web framework in the distribution. Django is available as version 3.2.12 with long-term support and offers asynchronous views and middleware, among other things. A word of caution: There is a risk of some incompatibility here during the upgrade. Ubuntu 22.04 also includes Go v1.18.x, Rust v1.58, and OpenJDK 11 for Java developers.

On the compiler side, Ubuntu has a great feature set with LLVM 14 and GCC 11.2.0. On the database side, PostgreSQL 14 and MySQL 8.0 impress with some new features. For PostgreSQL 14, stored procedures now return data via OUT parameters, simplifying the move from Oracle to PostgreSQL. MySQL admins can disable the audit log for sessions.

# Point of View

With every LTS release, Canonical explains what it considers to be the highlights of the new version, which allows conclusions to be drawn about what customers have been requested. This time, the company highlights native support for NVIDIA's vGPU software 14.0, among other things. This allows the virtual GPUs of many VMs to be linked together to accelerate machine learning and other scenarios with workloads that process serious amounts of data. In addition, Ubuntu 22.04 supports NVIDIA's AI Enterprise software suite, which offers advantages in a scientific context and high-performance computing. If you want to use Azure's confidential VMs, Ubuntu is the only Linux distribution that supports the feature. Multipass [9], a GPL software driven by Canonical, lets you start an Ubuntu VM on Windows, macOS, and Linux with a simple command and (now) also supports Apple's M1 chip. A real-time kernel (currently still in beta) is expected to find favor especially in the telecommunications industry, for example, for real-time applications in the 5G sector.

# Conclusions

If you are an admin or developer, you don't need to rush to switch to Ubuntu 22.04 LTS, but gradually transitioning only makes sense, even on your servers. You should consider making the switch not only because your favorite frameworks and content management systems will eventually switch to the new programming language versions, but also because updated software may utilize some of the new features that Ubuntu 22.04 delivers. If you want to wait, most of the teething troubles should be confined to history by the time the first point release, 22.04.1, appears. Before you make the change, check through the release notes [10] for the known issues taking your infrastructure into account. ▪▪▪

# Info

+   [1] HWE kernel: https://www.thomas-krenn.com/en/wiki/Ubuntu_LTS_Hardware_Enablement_Stack_information
+   [2] Kernel releases: https://www.kernel.org/category/releases.html
+   [3] Plans for Ubuntu kernel: https://discourse.ubuntu.com/t/ubuntu-desktop-gnome-plans-for-the-incoming-lts/26156/13
+   [4] NFS and UDP: https://www.mail-archive.com/kernel-packages@lists.ubuntu.com/msg473086.html
+   [5] SSH on older machines: https://bugs.launchpad.net/ubuntu/+source/openssh/+bug/1961833
+   [6] Ubuntu and OpenStack: https://ubuntu.com/blog/opensatak-is-dead
+   [7] OpenStack "Yoga": https://releasenotes.openstack.org/yoga/
+   [8] Kubernetes 1.23: https://ubuntu.com/blog/kubernetes-1-23-release-top-features
+   [9] Multipass: https://multipass.run
+   [10]Release notes: https://discourse.ubuntu.com/t/jammy-jellyfish-release-notes/24668