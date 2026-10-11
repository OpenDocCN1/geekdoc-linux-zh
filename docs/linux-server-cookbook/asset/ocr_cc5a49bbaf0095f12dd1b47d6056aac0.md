# # CHAPTER 10
## File Sharing

# ### Introduction

It is recommended to store files in a central location and share files between users and servers in a normal task inside enterprises. For example, a server can store some generated files in a central shared location, and a user can access a service, to access the file. Another use case is to have centralized storage for services, such as an image registry for containers.

Nowadays, with cloud services providing file sharing, such as Dropbox or Google Drive, the use of file sharing outside companies is not so popular. Companies that want to keep the files secure inside their own infrastructure and want to control access to the files will have to install and configure a file-sharing solution. Another popular use case at an enterprise level is to use file sharing for storing backups or providing dynamic storage for microservices.

The first part of this chapter will cover the most popular file sharing in Linux called **Network File System** (NFS). NFS is a popular distributed file system protocol to share files not only to end users but between systems or consumed by different services. This chapter covers how to install and configure the directories to be shared and the client options to access them.

The second part of the chapter covers the popular sharing protocol called **Server Message Block** (SMB), used in Windows and Linux. This chapter will cover the suite of programs called **Samba**, including the installation, configuration, and client tools to access the shared directories.

The last part of the chapter will cover a previously popular protocol called **File Transfer Protocol** (FTP), covering the installation of popular solutions for the service and the clients. The **Trivial File Transfer Protocol** (TFTP) and its use cases (that is, where it is used) will be described.

# ### Structure

In this chapter, we will discuss the following topics:

+   - NFS service and client