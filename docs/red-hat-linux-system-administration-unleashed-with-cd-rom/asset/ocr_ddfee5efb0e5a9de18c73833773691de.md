# An Open Source Solution

Now that we have defined a desired feature set and looked at a couple of manning strategies, we can take a look at a specific help desk solution available for Linux systems. While the solution we will be looking at does not have all of the desired features, it has most of them and because it is available under the GNU Public License and comes with source code, the missing features could be added if you desire. The most noticeable feature that is missing from the solution we are about to describe is an automatic escalation feature.

The solution we will look at for setting up a help desk is called WREQ and is in development at Duke University by Yunliang Yu and contributors from the user community to meet the needs of the systems administration staff there. It includes a simple Web-based interface for users as well as an email and command-line interface for expert users. It is implemented entirely in perl and is based on a similar product called REQ. The following sections take a look at how well this solution fits our desired feature set and then looks at a sample setup.

# The User Interface

The first requirement is a simple user interface for users. One advantage of the WREQ help desk system is that it is a Web-based solution, it can be accessed from any operating system or platform that supports a Web browser. The requirements for the Web browser are that it support frames and JavaScript, which is used to maintain state information. Figure 30.1 shows the WREQ issue entry screen.

A feature found in the WREQ system that makes it a better fit than some of the other systems of its type is the ability to manage multiple input queues or lists with a single installation.

In addition to this Web interface, WREQ also includes an email interface that allows you to work on issues in the absence of a Web browser. This email interface allows you to perform most of the functions of the Web interface by simply adhering to a simple syntax for the subject line. For example, if we set up WREQ and defined a list help desk, by sending email with subject lines as shown in Table 30.1 we can open, update, comment on, or resolve an issue.