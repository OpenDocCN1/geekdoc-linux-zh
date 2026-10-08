
## Continuous code analysis – part 1

Set up a Jenkins integration server ready for SonarQube analysis

![](img/c7d3278283754436651c50a2e9c72912_38_0.png)

![](img/c7d3278283754436651c50a2e9c72912_38_1.png)

### 01 Jenkins installation

Jenkins is available for download as a WAR file that can be dropped into your favorite JEE container or can be executed directly with a `java -jar jenkins.war` command. Note that JDK and JRE are prerequisites for Jenkins. If you'd rather not go deep into the details, you can also download the native package for your operating system. These packages contain the WAR file and the other dependencies required all together. You just have to download and install them like any other application. As soon as the installation completes, Jenkins is accessible at `http://localhost:8080/`. Note that there is no admin (or any other) user created because anyone can access anything. This will change only after Jenkins' security is set up, which is what we're going to take a look at next.

### 02 Get started with Jenkins

To set up security, go to Manage Jenkins > Configure Global Security and click on the Enable Security checkbox. The security settings will open up and here you can select the ports, on which other slaves can connect with Jenkins; the security realm, i.e. the user authentication method using LDAP, the Unix user group, Jenkins DB and more, and also the user authorisation (or in other words, the user permissions). Adding users depends on the security realm you select here. If you use the Jenkins database, an option to manage users in the Manage Jenkins page comes up automatically. Go to this page and click on the Create User link to add users. You may want to configure privileges and access levels for different users as you begin to add them. This can be done by heading across to Manage Jenkins > Configure Global Security > Access control > Authorisation > Matrix-based security.

Note that if you lock yourself out of Jenkins accidentally, you can simply open up the `/var/lib/Jenkins/config.xml` file and set the `<useSecurity>` element to false, and also remove the authorizationStrategy and securityRealm elements from the file. Save the file, restart Jenkins and you should be able to work.

### 03 Jenkins jobs

As a continuous integration server, Jenkins can take source code directly from your file system or even source code management system and then build it. This, along with pre- and post-build options and other features, enables you to experiment and configure tasks exactly as you need them. The various project builds/jobs supported by Jenkins are:

- **Freestyle software build**: It lets you use any SCM combined with any build process. You can also run shell/batch scripts, invoke and more while building the software. If you are not sure about the build type while setting up Jenkins, you should probably use this.
- **Maven**: Two-thirds of projects are specific to Maven projects and they analyse the `pom.xml` file in great details.
- **Multi-configuration project**: This will let you set up projects which may need more than one configuration, for example builds which are specific to different platforms. This is quite similar to the freestyle software build with an addition of configuration matrix which helps you set up different configurations.
- **Monitor an external job**: Jenkins can be used as a dashboard to monitor jobs run on external systems using this option. However, it may not be available by default, in which case you'll need to enable the external-monitor-plugin under the plugins page.

![](img/c7d3278283754436651c50a2e9c72912_39_0.png)

### 04 Setup SonarQube

Now that Jenkins is set up and you have a basic idea of what it’s capable of, let’s revisit SonarQube. SonarQube is comprised of three major components: the application source code hosted on a webserver, a database and the analyser. All three are logically separated and generally need to be installed separately. It’s the analyser that actually interacts with the source code to be analysed and saves the results to database. The SonarQube web interface then shows you the results. There are different analysers available for different project types. We will analyse a non-Maven Python project for demo using the SonarQube Runner. You can download it from the SonarQube website. Setting up the analyser requires editing the sonar-runner.properties file for database connection strings and credentials. If you get stuck, look up the first SonarQube tutorial: www.linuxuser.co.uk/tutorials/analyse-code-with-sonarqube.

![](img/c7d3278283754436651c50a2e9c72912_39_1.png)

### 05 Install SonarQube plugin in Jenkins

The plugin in question here is a Jenkins plugin, which enables it to connect to the SonarQube installation (specifically, the SonarQube analyser). After the connection is done, Jenkins can trigger the analyser based on predefined criteria. To install the plugin, open your Jenkins homepage and go to the Manage Jenkins > Manage Plugins page and click on the Available tab. Then search for ‘sonar’ in the filter box. As you type, you will see the Sonar plugin. Select the checkbox in front of it and click the ‘Install without restart’ button. Jenkins then starts the installation process, beginning with a network check and plugin download. Soon after, if everything is fine, the plugin gets installed. It needs to be configured now.

![](img/c7d3278283754436651c50a2e9c72912_39_2.png)

### 06 Plugin in action

To configure the plugin, go to the Manage Jenkins > Configure System and scroll down to the Sonar tab. Here you will need to fill in the name (SonarQube), its database credentials and other details. After filling this in, scroll up to the Sonar Runner tab and then fill in the Sonar Runner details here. This completes the setup. After the plugin is set up, go to the Jenkins homepage and create a new project. You can do this via the New Item link on the left, selecting ‘Freestyle project’ as the project type. In the configuration page that appears now, scroll down to the Build tab and select ‘Invoke Standalone Sonar Analysis’ in the ‘Add build step’ drop-down menu. Fill in the path of your project’s properties file (the same file required by SonarQube Runner to analyse a project). You can also select the trigger for building the project in the Build Triggers tab, just above the Build tab. This completes the process – now, as per your settings, Jenkins will automatically trigger the SonarQube analysis. To view it, just need to log in to SonarQube and the latest code quality metrics will be available to you.

> "Jenkins generally needs a restart after any configuration changes or after any plugin installations"

![](img/c7d3278283754436651c50a2e9c72912_40_0.png)

![](img/c7d3278283754436651c50a2e9c72912_40_1.png)

### 07 Job Config History plugin

This plugin is especially helpful for people who are new to Jenkins, though people with some experience on Jenkins may also find it useful. Let's consider a scenario – your Jenkins build works fine, then you think of making further improvements and start changing the settings, and suddenly everything stops working. But you don't even remember the last change you made! Well, JobConfigHistory plugin is there to bail you out of such situations. It saves the config.xml after each change you make in Jenkins settings. You can just check the file differences and make necessary amends.

### 08 SafeRestart plugin

Jenkins generally needs a restart after any configuration changes or after any plugin installations. But being a server-client-based application with multiple concurrent users executing their jobs, you need to be extra careful since you may accidentally abort someone else's build during a restart. The SafeRestart plugin frees you from worrying about this. Once you click the 'Restart Safely' button (that appears in the left menu bar after you install the plugin) it schedules a restart once all the builds are done.

![](img/c7d3278283754436651c50a2e9c72912_40_2.png)

### 09 Ownership plugin

As the name suggests, this plugin lets you assign explicit ownership for jobs and slave nodes. Introducing ownership means better responsibility management and faster resolution of issues... unless it turns into pointing fingers! On a serious note though, this plugin definitely offers a good way to handle issues – after a job fails you don't need to find someone to fix it. After you install this plugin, you get a link on the left menu bar called Manage Ownership (when inside a project). Here you can configure the owners/co-owners of a respective job.

![](img/c7d3278283754436651c50a2e9c72912_40_3.png)

### 10 Google Calendar and compress artefact plugin

The Google Calendar plugin allows you to publish build records to Google Calendar. After you install the plugin, you can view the option to publish build status to Google Calendar in the postbuild actions tab. A form appears as you select it and you then need the calendar URL and your credentials to fill it. After that, Jenkins automatically pushes the build results to your Google Calendar. Simple and effective! If you plan to save the build artifacts such as the test logs and build files after each build, you may find this plugin useful. This plugin compresses the artifacts before saving them to the disk, thus saving the disk space for you.
