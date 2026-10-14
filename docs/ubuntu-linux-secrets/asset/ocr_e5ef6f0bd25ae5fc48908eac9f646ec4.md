Over the years, email has become the "killer app" of the Internet. These days, just about everyone has an email address, and many people have more than one! The Ubuntu server provides a great platform for creating your own email server, whether it's for you or for a small business or organization. It uses the popular Postfix email server to process messages from internal users on the server and from external mail sources. This chapter first describes how email works in the Ubuntu environment and how Ubuntu uses Postfix to handle email as a server. It then looks at how to configure Postfix and procmail (a popular mail delivery tool) to work in your specific email environment.

# How Email Works

When you send an email message to your Aunt Betty, it passes through several programs along the way before she gets to view it in her email client program. Different types of operating systems handle email differently. The Linux operating system breaks the function of Internet email into separate processes that are each handled by separate programs. Figure 23-1 shows how most Linux email software (including Ubuntu) modularizes email functions.

![](bbox=[0.22, 0.56, 0.68, 0.85])

Figure 23-1: Linux modular email environment.