A coworker, Dr. Brown, has come back from DevOps training and proposes a radical (at least for them) way to shift their company's development and production process. He suggests the following:

+   1.  The development team employs a container for their environment to create Future app changes.
+   2.  The production application environment is also moved to a container, and its image is put into a registry for container version control.
+   3.  The Future app production container is replicated, with each replication running to meet customer demand using a tool such as Kubernetes.
+   4.  The development container's configuration and security policies are determined by Marty and Jennifer's team and recorded (infrastructure as code) in a tool, such as Puppet or SaltStack.
+   5.  Instead of massive changes to the Future app, Jennifer's team will create small incremental changes to the code and use a version control system, such as Git.
+   6.  These small software code changes are tested automatically via a tool, such as CircleCI or Jenkins.
+   7.  The tested modifications are released on a weekly basis.
+   8.  After the testing and development have been completed on the app development image, it is moved into the container registry for version control.
+   9.  The current Future app production container images are stopped and the development containers take their places. This is done so that the Future app users experience no outages. If needed, Marty can roll back to the old production container image should problems arise.
+   10. On the production containers, the Future app is monitored and data logged to track performance and other metrics, using a tool such as Splunk. Performance events or container outages may automatically trigger the replication of additional production containers.
+   11. Jennifer and her development team create a new Future app development container image for more customer-requested modifications, and the process is started all over again.

The result of this DevOps implementation greatly reduces the Future app's software errors, increases the speed of desired customer modifications into production, and improves the communication between the tech ops and software development team. Overall, it is a win-win, as many companies are discovering today.