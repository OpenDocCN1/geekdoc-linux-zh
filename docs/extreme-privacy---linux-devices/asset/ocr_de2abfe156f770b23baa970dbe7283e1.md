![](bbox=[0.35, 0.08, 0.65, 0.1])

![](bbox=[0.13, 0.11, 0.87, 0.39])

# Twilio Sanitization Script

I previously explained the reasons Twilio is my preferred VoIP provider. If you use your Twilio numbers often, manually sanitizing the data stored on Twilio's servers is quite time consuming. I possess an automated script which conducts all actions on my behalf, and presents information about my account when needed, all without logging into my Twilio account. Let's start by installing Twilio's CLI tool with the following steps. This should only be applied if you have a Twilio account.

+   - Navigate to `https://github.com/twilio/twilio-cli/releases`.
+   - Expand the latest "Assets" area until you find one with an "amd64.deb" file.
+   - Download the file, similar to "`twilio-5.10.0-amd64.deb`".
+   - Right-click the downloaded file, select "Open with Eddy", and click "Install".

Once installed, execute the following within Terminal.

```
`twilio login`
```

This will ask for your Twilio SID and Token, which can be found in your portal. When prompted, provide a name of "CLI". Next, execute the following.

```
`twilio profiles:use CLI`
```

This generates the appropriate configuration file which tells your computer to use this profile with the provided credentials for all future commands. You can now manually interact with the Twilio CLI using the following Terminal commands.

```
`twilio phone-numbers:list`
`twilio api:core:calls:list`
`twilio api:core:messages:list --properties='sid,from,body'`
`twilio api:core:recordings:list`
`twilio api:core:transcriptions:list`
```

We can now automate the sanitation steps within a script which can be downloaded and installed with the following Terminal commands.

```
`cd ~/Documents`
`wget https://intellechiques.com/data/twilio.sh`
`chmod +x twilio.sh`
```