# CAA by Example

In the last chapter we discussed the details of how CAA works. In this chapter we will discuss how to implement application resources for some common tasks.

+   - A simple highly available resource
+   - A highly available resource with dependencies
+   - A highly available resource with CFS Server Relocation
+   - A highly available resource that requires privately-mounted file systems
+   - A highly available resource that requires managing its own cluster alias
+   - A non-highly available resource that is used to automatically (re)start an application
+   - Mutually exclusive resources
+   - Creating a resource using SysMan

# 24.1 Creating a Resource – Step by Step

Once you have determined that you need a resource in order to achieve a highly available application, here are the steps that you must take to create, register, and start a resource.

+   1. Create a Resource Profile
+   2. If you created an Application Resource, create an Action Script
+   3. Test your Action Script
+   4. Validate the Resource Profile
+   5. Register the Resource with CAA
+   6. Start the Resource

# 24.2 Simple, Highly Available Resource

A simple, highly available resource can be defined as an application resource that manages one application.