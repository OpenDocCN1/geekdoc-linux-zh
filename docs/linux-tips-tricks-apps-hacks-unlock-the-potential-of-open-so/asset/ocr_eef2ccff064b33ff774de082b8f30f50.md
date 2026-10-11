# Tips | Tricks | Hacks | Apps

# 03 Taiga-front installation

For the next step, let's complete the Taiga frontend installation. Taiga uses various programming languages other than the usual CSS/HTML/JavaScript in the frontend, so it really needs to be built before your browser can fully understand it.

Download Ruby and Gems. After setting the path with the last command, restart the shell with the following:

```
sudo apt-get install -y ruby
gem install --user-install sass scss-lint
export PATH="~/.gem/ruby/1.9.1/bin:$PATH"
```

Now complete the NodeJS installation with:

```
sudo apt-get install -y nodejs npm
```

Then you will have to run the `node` command to check if the command is recognised. If this isn't the case, you should run:

```
sudo ln -s /usr/bin/nodejs /usr/bin/node
```

Now install gulp and bower:

```
sudo npm install -g gulp bower
```

...then get the code and compile taiga-front:

```
cd -
git clone https://github.com/taigaio/taiga-front.git taiga-front
cd taiga-front
git checkout stable
```

Compile using:

```
npm install
bower install
gulp
```

Now run gulp:

```
cd -taiga-front
gulp
```

If you find that you have npm errors while running gulp, clear the temp files and install all dependencies again.

```
rm -rf ./.npm; rm -rf node_modules
npm install
bower install
gulp
```

If it is successful, you should now be able to see Taiga on http://localhost:9001.

![](bbox=[0.38, 0.18, 0.88, 0.43])

# 04 Create project and user stories

> “Sprints have predefined time slots, usually two to three weeks”

![](bbox=[0.38, 0.52, 0.62, 0.66])

With Taiga now running in your browser, the next step is to create a project. We already have the admin user created with the password 123123, so log in to Taiga with the credentials and click on Create Project. Then select the Scrum template and click Next. Finally, fill in the relevant details (name and description) and click Create.

This will take you to the Project Backlog page. On the upper half of the page you have the burn-up chart and the lower half has the user story list. On the right sidebar, you can see the Sprints section. As is generally done, let's start with creating user stories, since the untinted, agile development methodology requires software features to be broken down into smaller units based on a user's point of view. These units are called user stories in agile jargon.

To add a user story, just click 'Add a new user story' in the lower half of the page. On the next page, fill in the details. Note that you can assign project points to the user story via this page. You can also add several stories at once using the bulk insert button (next to the 'Add a new user story' button), and do not forget to change your admin password to something memorable!

# 05 Create sprints

Now that the user stories are available, let's plan the sprints. As you may be aware, sprints are predefined time slots, usually two to three weeks. Before a sprint starts, developers commit a set of user stories to be finished by the end of the sprint. When the sprint is over, scrum master takes stock of the situation and decides the user stories for the next sprint, and this cycle continues.

To create a sprint in Taiga, just click the New Sprint button on the right sidebar. On the next page, fill in the name and the duration of the sprint. By default, sprints are of two weeks – the start and end date gets filled automatically. Since you have already added user stories, just go to the backlog page, select the relevant user stories and click the 'Move to current sprint' button. Thus you can have stories assigned to the sprint and the rest of the stories available as backlog. Once you have user stories assigned to sprints, you can further break it down to dependent tasks.