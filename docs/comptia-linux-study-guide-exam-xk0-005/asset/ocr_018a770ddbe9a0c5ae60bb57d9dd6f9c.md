created with preset library and operating system versions and security settings. All these settings are recorded. No software updates (such as via a sudo apt-get dist-upgrade command) are issued within the image.

**Version Control** After the software development process and prior to moving a modified app container image into production, the container and its recorded configuration are registered with a version control system. The version control system can contain previous app container images, including the one currently in production. Some companies use a manual version control system implemented with backups.

**Replace Not Update** After registration, the app container is ready to move into production. Instead of the production app container image being updated to match the development image, the production container is stopped. The development app container image then replaces the production container and starts as the production environment. Thus, an environment switch occurs.

**High Availability** *Replication* is the process of creating multiple copies of the production app container image and running them. This allows you to stop old currently unused production app containers and replace them with the new production app containers, which provides continual uptime for your app users. With containers and replication, the old method of shutting down your production environment to update it during a time period in the wee hours of the morning is gone.

To accomplish these tasks with container images, you need orchestration. Orchestration principles provide tools, utilities, and guidance for implementing app container images in a fast-paced environment, such as one that uses DevOps.

# ## Real World Scenario
### Moving to DevOps and Orchestration

Marty is a tech ops lead. He is in charge of managing the systems that support his company’s primary application, called Future.

Jennifer is lead programmer on the Future app. She and her team make desired enhancements and fix bugs in its software. When her team has completed its modifications and testing of the app, it is moved into production on Marty’s systems.

Unfortunately, in this environment, problems ensue. Jennifer’s development computers are not kept in sync with Marty’s production systems as far as server, operating system versions, and libraries are concerned. This introduces additional bugs into the Future app code and causes lots of extra work for both Jennifer and Marty. In addition, customer-desired modifications are very slow to move into production. Marty and Jennifer tend to blame each other.