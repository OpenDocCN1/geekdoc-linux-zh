
## Work with Python

## Bug-sweep your code with SourceClear

Keep your software projects safe — learn how to find and fix library-based security vulnerabilities quickly and easily

![](img/e016e192a91ffc1a9e474690a590742f_89_0.png)

```bash
vagrant@vagrant-ubuntu-trusty:64:~$ sudo apt-get install srcclr
Reading package lists... Done
Building dependency tree
Reading state information... Done
The following NEW packages will be installed:
 srcclr
0 upgraded, 1 newly installed, 0 to remove and 38 not upgraded.
```

be installed on nearly any Linux-based operating system by running one of the following sets of commands:

```bash
curl -sSL https://sourceclear.com/install | bash
```

Or, via apt-get if you prefer:

```bash
sudo apt-key adv --keyserver keyserver.ubuntu.com --recv-keys DF7D7A50B746DD4
sudo add-apt-repository "deb https://download.srcclr.com/ubuntu stable/"
```

![](img/e016e192a91ffc1a9e474690a590742f_89_1.png)

```bash
sudo apt-get update
sudo apt-get install srcclr
```

### 01 Install the SourceClear Agent

The SourceClear command-line interface (CLI) agent is a flexible utility that allows for easy scanning of your code projects for vulnerabilities in open-source. The tool can

The average software project today relies on dozens — sometimes hundreds — of open source libraries. Are those libraries up to date? Are there any security vulnerabilities in the versions you're using? How would you even know?

SourceClear makes it easy to answer these questions and more, automatically. You'll get complete analysis of your open-source dependencies – security vulnerabilities, out-of-date libraries, and license reports.

To analyse your project, we'll be using the SourceClear command-line agent. By tapping into the native build and package managers that manage open-source dependencies, we'll start by gathering information on the full dependency graph. We'll then match up those libraries to the SourceClear Registry – the largest database in the world of open source security vulnerabilities – and help you triage the issues we might find.

Let's start by looking into a popular Python project and seeing what we can uncover.

### 02 Activate your SourceClear Agent

To activate your agent, we'll need your activation token from **SourceClear.com**. From the New Agent page, you can select your operating system (i.e. Linux). Copy your activation token by clicking on the clipboard to the right of the field. Next, go back to your terminal and run the following command, entering your activation token when prompted:

```bash
srcclr activate
```

This will create a configuration file with your API token in `~/srcclr/agent.yml`. If you wish to use this agent on another environment, you can copy the API token from this file and set it to the `SRCCLR_API_TOKEN` environment variable on another system without needing to activate the agent again.

### Resources

- **Linux or OSX machine with internet access**
- **Python 2.7.x and pip installed on the local path**
  - www.djangoproject.com/download
- **Git 1.9.3+**
- **A free SourceClear.com account**
  - https://www.sourceclear.com/

![](img/e016e192a91ffc1a9e474690a590742f_90_0.png)

### 03 Test your environment

Let's ensure that your local environment is set up for scanning Python projects by running the following command:

```bash
srcclr test --pip
```

> To demonstrate how SourceClear works, we'll start by analysing a public Python project called Mezzanine

This command will display assorted system information that is used by the SourceClear CLI, and perform a scan of a test project that uses the specified package manager (pip in this case). The package manager information listed is only required if you wish to scan a project that uses libraries from the specific package manager. After running this command, you should now see output looking similar to the screenshot seen below.

![](img/e016e192a91ffc1a9e474690a590742f_90_1.png)

### 04 Scan your Python project

To demonstrate how SourceClear works, we'll start by analysing a public Python project called Mezzanine (https://github.com/stephenmcd/mezzanine), which is a popular content management system built on Django.

We can scan projects like this by using their GitHub URL:

```bash
srcclr scan --url https://github.com/stephenmcd/mezzanine
```

Specifying the GitHub URL will perform a shallow clone of the project, scan it, and then remove the project once finished. To scan projects you have locally, just use the path; for example:

```bash
srcclr scan /path/to/mezzanine
```

### 05 View the scan report from standard output

After scanning the project, the output provides an overview of vulnerability and GPL licensing information. For this particular scan, the Django 1.8, requests 2.2.1, and Pillow 2.3.0 Python libraries are associated with 30 different vulnerabilities. In addition, the code in this particular project is actually using the vulnerable method associated with a Django 1.8 vulnerability.

### 06 Review the full scan results

The standard output from the SourceClear agent is helpful, but let's take a look at the full report online. Copy the Full Report Details URL at the bottom of the output and paste it into your browser. Once you've logged in, you can see the full details of this scan, including detailed vulnerability information, license information, and a searchable list of the open source libraries that are being used. All of the data can be filtered based on attributes of the library, license, or vulnerability (i.e. only high risk vulnerabilities, out of date libraries, and so on).

![](img/e016e192a91ffc1a9e474690a590742f_90_2.png)

### 07 Fix a security issue

SourceClear integrates with JIRA and GitHub issues to help you track and fix vulnerabilities. In our report, we've identified a security issue that is not just part of this project, but one where the Mezzanine code directly calls the methods that are vulnerable. This is crucial to fix. We're going to create a GitHub issue for this vulnerable method by clicking the

### Security automation made easy

Scanning projects from your laptop is a great way to get started, but automating the process helps the whole team. Adding security to your workflow can be made easy when you add SourceClear scanning inside your Continuous Integration environment. Just set up your activity token and add a post-built task. You can get environment-specific instructions over at https://www.sourceclear.com/doc/

checkbox next to the vulnerability and then selecting the Create Issue button.

![](img/e016e192a91ffc1a9e474690a590742f_91_0.png)

![](img/e016e192a91ffc1a9e474690a590742f_91_1.png)

### 08 View vulnerability details

Now that we’ve identified the vulnerability, we want to fix it. SourceClear provides detailed information for the vulnerabilities. We can see this by going to the Issues tab within the scan report and clicking the vulnerability we want to fix. This will display a page with a description of the vulnerability, the library it is found in and the full call chain for any vulnerable methods that might be used and how to fix it.

### 09 Look at the vulnerable code

Viewing the vulnerability fix information allows us to see exactly where in the code the vulnerable part is being used. In order to see how vulnerable caller #2, `next_url`, is being used, we can go to line 97 within the `url.py` file. Sure enough, the vulnerable `is_safe_url` function is being used within the `next_url` function as shown in the screenshot.

![](img/e016e192a91ffc1a9e474690a590742f_91_2.png)

### The Fix

Using our understanding of where this vulnerability occurs in the code allows us to decide if altering the code itself to remove the vulnerability would be the best solution.

![](img/e016e192a91ffc1a9e474690a590742f_91_3.png)

### 10 Fix a vulnerability

Fixing this particular vulnerability by changing the code does not look to be the most feasible option in our case. Instead, we have the option of viewing the vulnerability fix information in SourceClear to see how to update the library in use to a version without any known vulnerabilities. The version that SourceClear is recommending to us is free of known vulnerabilities, so updating will only require that you specify a library version range greater than or equal to the suggested version.

### 11 Apply the fix

Updating a library can be tricky, especially if the library is indirectly used in your code (i.e. library A depends on library B, which happens to be vulnerable). Fortunately the Django library is directly specified in the `setup.py` file within the project’s root directory, which means we can simply update the version range for this particular library. As of November 2016, versions 1.10.3 or higher of Django do not have any known vulnerabilities.

![](img/e016e192a91ffc1a9e474690a590742f_91_4.png)

### 12 Test your changes

It is important to verify whether or not your project is compatible with a newer version of a library prior to
