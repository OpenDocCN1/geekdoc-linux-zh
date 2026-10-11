
# Organise collaborative projects with Ganib

Discover how to install Ganib and use it to manage and simplify your collaborative projects

![](img/628186dda7facdc011bf39c938de3975_39_0.png)

**Nithish Tiwari** is a software developer by profession, with a huge interest in free and open source software. As well as serving as community moderator and author for leading FOSS publications, he also helps organisations adopt open source software for their business needs.

## Resources

- Ganib
- http://www.ganib.com/

![](img/628186dda7facdc011bf39c938de3975_39_1.png)

**Software development is one of the fastest growing fields in IT, but it has its own problems.** There are remotely distributed teams, working on the same code repository. There are changing priorities and deadlines. There are changing requirements and new technologies coming up. In addition, with its intangible outputs, software development proves very difficult to measure. So how do you manage all this while making progress?

![](img/628186dda7facdc011bf39c938de3975_39_2.png)

Agile development methodology has given us some hope. Agile focuses on the end product, while ignoring trivial things like lines of code written or man-hours spent, thus eliminating the need to measure effort and rather measure the completion of the final product. But then there is a dearth of good open-source, agile-focused tools; most of the tools are old, tweaked to support agile. With Ganib, this is set to change. Ganib is an open source project management tool with support for agile scrum, real-time tracking, bug tracking and various other features. It also supports integrations with third party tools like Microsoft Project, LDAP and so on to facilitate seamless working. In this tutorial, we'll take a closer look at Ganib and its features. But before that, let's start with the installation process. We've used Ubuntu 14.04 as the platform of choice for installation.

### 01 Installation preconditions

Ganib can be installed on any of the major OS platforms. As mentioned earlier, we have taken Ubuntu 14.04 as the base platform for this tutorial. To get started, you should have JRE and MySQL installed on your system. Apache Tomcat is required as well, but it is bundled along with the Ganib installer. So, let's first see how to install MySQL. The installation is simple; update your package index, install the mysql-server package, and then run the included security and database initialisation scripts. Just open a command prompt and type the following commands.

```bash
$ sudo apt-get update
$ sudo apt-get install mysql-server
$ sudo mysql_secure_installation
$ sudo mysql_install_db
```

> **Above right**
> The Ganib homepage depicting various features. In the middle, you have the burn down chart, followed by the billing hours

Once done, let’s check if you have JRE installed already. Type

```bash
$ java -version
```

If you get an error saying “the program ‘Java’ can be found in following packages”, it means you don’t have JRE installed yet. To install JRE, first update the package index

```bash
$ sudo apt-get update
```

Then install JRE.

```bash
$ sudo apt-get install default-jre
```

Once this is done, it is a good idea to install JDK as well.

```bash
$ sudo apt-get install default-jdk
```

### 02 Ganib installation

Now download the latest Ganib installation package from SourceForge. Here is the link http://sourceforge.net/projects/ganib/files/latest/download/latest.zip.

Unzip the downloaded file to the location where you’d like to install Ganib. You can do this using the commands below:

```bash
$ cd <Target Directory>
$ unzip Ganib-5.3_with_jre.zip
$ cd Ganib-5.3_with_jre
```

Then, import the database script files to your MySQL installation. But first, create a database for Ganib. Here is how to do it:

```sql
$ mysql -u root -p
mysql> CREATE DATABASE ganib CHARACTER SET utf8 COLLATE utf8_general_ci;
mysql> exit;
$ mysql -h localhost -u root -p ganib < database/ganib.sql
```

![](img/628186dda7facdc011bf39c938de3975_40_0.png)

#### Import/Export MSP

> If you switched to Ganib recently and your project plan is saved in Microsoft Project, you can easily import your MS Project files into Ganib. To do this go to the Plan module, and hover over the MSP link. You’ll see options to Import and Export MSP. You can also share your plans with customers/partners in MSP file format by exporting it to MSP.

Next edit the Tomcat/conf/context.xml file to change the database connection properties.

```xml
<Resource name="jdbc/GanibDB" auth="Container"
type="java.sql.DataSource" username="root"
password="" driverClassName="com.mysql.jdbc.Driver"
url="jdbc:mysql://localhost:3306/ganib?autoReconnect=true&useUnicode=true&characterEncoding=utf-8" maxActive="125" maxIdle="25" />
```

Don’t forget to change the username, password and the database name as per your setup. We’re assuming you’re installing Ganib on localhost, so we’ll also need to change the SMTP settings. So, edit the same file as above and also update the following:

> “Though time tracking is crucial for a project it is also very time consuming to enter data manually after each task”

```xml
<Resource
name="mail.GanibSession"
type="javax.mail.Session"
auth="Container"
mail.smtp.host="localhost"
mail.smtp.auth="false"
mail.smtp.user="username"
password="password"
mail.smtp.port="25"
mail.transport.protocol="smtp"
/>
```

Now, to start Ganib, run

```bash
$ chmod +x Start_Ganib.sh
$ ./Start_Ganib.sh
```

If everything is fine, you’ll be able to access Ganib at localhost:8080 on your browser.

### 03 Getting started

Now that Ganib is successfully installed and you can access the homepage on your browser, let’s get started with its basic usage. First, we will create an account. Once logged in to the Ganib application, you will be asked to provide an account name and account description in the home page. Provide the relevant information and on submitting the required data, you will see an account dashboard page for the new account. Next we create user accounts for the members of the project. Once you are inside an account, select the Resources button on the top menu bar. You can enter first name, last name and email address for the project members here. Once done, select and invite them as member, leader or manager. Ganib allows role-specific information access. For example, data that a manager can access need not be disclosed to all project members. Multiple roles can be added to a single user. Typically, users are added at the beginning of the project but you can add them during the project too.

![](img/628186dda7facdc011bf39c938de3975_41_0.png)

![](img/628186dda7facdc011bf39c938de3975_41_1.png)

#### Theme and colours

You can change the theme colour of your Ganib application from the footer, or any webpage you’re on. There are several options available: the major ones are blue, orange or green. To do this, just click ‘Change Theme’ in the footer and you’ll see a colour palette pop-up from the right. Just select the colour of choice and the theme will change.

Ganib provides a user-friendly interface for timesheets where project members can easily update their current tasks or view tasks for any data, week or month. Monthly views allow you to keep track of what an employee has worked on and for how many hours in that month. You can easily navigate to a certain date of a month to view the task details and also select a different month or year. There are few filters available in the page to view the desired data for particular account and project.

Ganib timesheet also provides you with weekly views where you can see tasks assigned to logged-in users and meetings scheduled in that week. You can easily navigate between weeks and select the date range from the filters to view data for a particular week. You can further filter out data based on name and assignment types.

![](img/628186dda7facdc011bf39c938de3975_41_2.png)

![](img/628186dda7facdc011bf39c938de3975_41_3.png)

### 04 Create a project

Now we have an account and project members allocated to that account. Next we create a project in Ganib. On the Account page, you’ll see the icon for creating a new project. Click on the icon and enter the project name and description to create the project.

When the project is created, the next thing is to create a task plan to help manage the project easily. Ganib provides a plan module where you can easily create a task and change its dates, dependencies, deadlines and assignments to anyone for specific hours/day. As you start working on the task you can update the number of hours spent per day on the task along with any comments you want to specify.

### 05 Time management

Time management is the most crucial part for effectively managing a project. Click on the Timesheet button on the top menu bar to access timesheets.

### 06 Generating reports

Project progress can be monitored using reports. Reports are also very effective tools for managers for purposes like budgeting and estimations, where developers can view statistics based on task status, and monitor if they are behind deadline or on track. There are several detailed reports available in Ganib. To access reports click on the Reports button on the top menu bar.

> “During almost all the phases of a project’s life cycle, documents play a very important role. File management is often a burden for a project manager”

When a complex task is created it is very difficult to manage it between the team due to confusion that arises when multiple people are working on it. Using Ganib you can easily manage complex tasks by turning them into simple sub-tasks, which will help each team member to concentrate on one thing at a time.

There are two major bar graphs available. First is the work-based bar graph, depicting the percentage of work completed on a particular task. It classifies the tasks into categories: percentage-of-completion, late and unsigned tasks. Second is the members-based bar graph. This bar graph gives details on all of the resources in the project. It even classifies the users according to their availability status as online, active and inactive (resources who are offline for more than eight hours).
Apart from these there are also four more graphs available – Billed Hours showing the hours calculated for each user on each...
