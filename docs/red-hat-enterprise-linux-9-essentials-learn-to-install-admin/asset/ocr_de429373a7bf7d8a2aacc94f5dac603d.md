as groups of interacting modules, each running in a separate container.

One possible drawback of containers is that the guest operating systems must be compatible with the version of the kernel being shared. It is not, for example, possible to run Microsoft Windows in a container on a Linux system. Nor is it possible for a Linux guest system designed for the 2.6 version of the kernel to share a 2.4 version kernel. These requirements are not, however, what containers were designed for. Rather than being seen as limitations, these restrictions should be considered some of the key advantages of containers in providing a simple, scalable, and reliable deployment platform.

# 27.3 RHEL 9 Container Tools

RHEL 9 provides several tools for creating, inspecting, and managing containers. The main tools are as follows:

+   - **buildah** – A command-line tool for building container images.
- **podman** – A command-line based container runtime and management tool. Performs tasks such as downloading container images from remote registries and inspecting, starting, and stopping images.
- **skopeo** – A command-line utility used to convert container images, copy images between registries and inspect images stored in registries without downloading them.
- **runc** – A lightweight container runtime for launching and running containers from the command line.
- **OpenShift** – An enterprise-level container application management platform consisting of command-line and web-based tools.

All of the above tools comply with the Open Container Initiative (OCI), a set of specifications designed to ensure that containers conform to the same standards between competing tools and platforms.

# 27.4 Container Catalogs, Repositories, and Registries

The Red Hat Container Catalog (RHCC) provides a set of pre-built images tested by Red Hat that can be downloaded and used as the basis for your own container images. The RHCC can be accessed at the following URL and allows searches to be performed for specific images:

https://catalog.redhat.com/software/containers/search

After completing a search, the catalog will display a list of matching repositories. A repository in this context is a collection of associated images. Figure 27-2, for example, shows a partial list of the container image repositories available for RHEL 9 related containers: