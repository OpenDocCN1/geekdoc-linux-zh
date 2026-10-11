# # Configuring the Virtual Office Environment

The Services Administration tasks you just learned about are primarily focused on integrating the various NNLS components and configuring the user interface. The Virtual Office Environment Administration tasks covered here are used to configure the behavior of the Virtual Office service itself.

The Environment Administration task is located beneath the Virtual Office role in iManager. Using this task, you can configure virtual team parameters as well as set logging levels. Let's look at each of these functions.

> > **WARNING**
> > You'll notice as we go through this section that a third function is available in the Environment Administration screen: configuring portal information. We're not going to cover these parameters here. The Virtual Office software engineers at Novell have indicated that the average user shouldn't touch these settings unless a Novell Support Engineer has directed him or her to do so.

# ## Setting Team Configuration Parameters

Before talking about how to configure team parameters, we need to discuss exactly what a team is. Virtual Office allows users to create *virtual teams*. These teams allow employees in an organization to collaborate through email, real-time chat, file sharing, and calendaring.

An end user can create a virtual team from within his or her Virtual Office home page. When this happens, the user who created the team becomes the owner of the team and the first team member. The team owner can then invite other users to join the team as members. The invitees will be sent notification and given the opportunity to accept or decline the invitation to join.

You can control, to an extent, the way teams are handled by Virtual Office by configuring team parameters in iManager. To do this, you need to complete the following steps:

+   1. Open iManager and scroll down to the **Virtual Office** role.
+   2. Select the **Environment Administration** task. The screen in Figure 11.38 is displayed.