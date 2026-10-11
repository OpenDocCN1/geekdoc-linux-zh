![](bbox=[0.17, 0.09, 0.84, 0.44])

The layers represented in figure 13.3 are as follows:

+   - Base Image with Debian
+   - Adding configuration to the Base Image
+   - Installing Apache in the previous layer

A Container based on this generated Image will be based on the Debian base image and will have configuration added. Apache is also installed. Any Image can be used by several containers at the same time. An Image has a history track and version control, and this helps show what changes were made in each layer. It is possible to go back to a previous version of it.

Cloud Providers, such as AWS or Google Cloud, offer the possibility to run containers on their platform. This is an ideal solution for customers who do not want to maintain a platform and want to modernize their applications.

Image registry