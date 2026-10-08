
## Work with Python

  committing changes. In this particular case, the version of Django we are updating to is below the highest version constraint (1.11), so the changes should not break the project. To be sure, you can use the Coverage Python library to run the tests for your project. As shown in the screenshot, the tests were successful, which means we can proceed with changes knowing that the project works as intended, assuming the appropriate test coverage is implemented.

```
vagrant@vagrant-ubuntu-trusty:64: ~/teamzinnine5$ scnr scan --allow-dirty
SourceClear scanning engine ready.
Running the PIP scanner
```

### 13 Scan before committing

Once we have tested the fix, we can verify that the vulnerability fix worked prior to committing it to source control by running another SourceClear scan. SourceClear requires all code changes be associated with a commit in order for results to be sent and tracked in the web platform. By using the `--allow-dirty` argument, you can scan a project with uncommitted changes without sending the results to the web platform in order to verify that a vulnerability is fixed.

![](img/e016e192a91ffc1a9e474690a590742f_92_0.png)

### 14 Verify the fix worked

After scanning with the `--allow-dirty` option, you can see an overview of the results and observe whether or not the vulnerabilities you intended to fix show up in the results. In this case, the output displays no vulnerabilities related to Django, which confirms that the changes were successful. Unfortunately, there are still vulnerable libraries being used in this code. Though the vulnerable methods for the libraries are not being used, we would still like to update to a non-vulnerable version to ensure that someone else contributing to the code does not use the vulnerable method.

### 15 Fix the rest of the vulnerabilities

In the SourceClear dashboard, within the Issues section, you can select the Updates tab in order to view libraries that are out of date and are referenced directly by the dependency requirements file (setup.py, requirements.txt, pom.xml, etc). The remaining two vulnerable libraries, Pillow and requests, have version range requirements that do not specify an upper bound. This means we can simply

| Scan | Library (Direct Only) | Version In Use | Latest At Scan |
| :--- | :--- | :--- | :--- |
| 6509584 | ipynb2 | 1.9 | 1.10.3 |
| 6509584 | requests | 2.2.1 | 2.11.1 |
| 6509584 | Pillow | 2.3.0 | 3.4.2 |

update the constraints to be greater than or equal to the latest version displayed in the Latest At Scan column.

### 16 Update your libraries

Now that you know the versions to update to, you can change the version ranges so that they are greater than the specified Latest At Scan version. After updating the version ranges, you should run another scan with the `--allow-dirty` argument to ensure updates fix was successful. Often you might find that version updates will cause more dependencies to be identified by SourceClear, because the library being updated might have another dependency it also depends on. SourceClear refers to these as “transitive” dependencies.

![](img/e016e192a91ffc1a9e474690a590742f_92_1.png)

### 17 Scan the committed changes to SourceClear

Finally, you will have identified and fixed all of the vulnerabilities associated with the project you are working on. By going into your Issues tab, the project sees that your code is now free from known vulnerabilities. You can easily add SourceClear into your CI pipeline as well in order to automate this process, and keep your issues tab up to date with vulnerability information.

![](img/e016e192a91ffc1a9e474690a590742f_92_2.png)

### 18 Notifications for future vulnerabilities

Security for your code is a constant battle, and it is important to make sure you are aware of any added vulnerable dependencies or newly identified vulnerabilities in your code. You can make sure you are notified by selecting the drop-down by your username in the top-right corner and choosing Notification Settings. You have the option to enable a weekly email summary of vulnerability information across all of your projects, or immediate notification emails when a new vulnerability is introduced to any of your code, or both. Congratulations, your open source libraries are secure!

![](img/e016e192a91ffc1a9e474690a590742f_92_3.png)

### JSON output

Want to integrate SourceClear data into other security tools or dashboards? The SourceClear agent can produce scan data in JSON format – just use the `--json` argument when you run a scan. This data can be piped to a file or used in combination with a script to fail builds automatically when SourceClear identifies certain vulnerabilities or libraries.

## Copy: A cp to call your own

Take inspiration from the common mocking bird and learn how to develop a light version of cp in Python 3 and safely copy files.

Here, we'll be showing how to implement the cp command line utility in Python 3 – and our Python version will be called pycp.py. All operating systems offer at least one way to copy files and Linux is no exception. To understand how essential the cp command is, you should know that it is located inside /bin, which is available even if you boot your Linux machine in single user mode.

```python
sys.exit(0)

if os.path.isdir(what):
    print(what, 'is a directory!')
elif os.path.isfile(what):
    print(what, 'is a file!')
```

The os.path.isdir() method tells whether its parameter is a directory or not whereas the os.path.isfile() tells whether its argument is a regular file or not. It should be noted here that although it looks redundant to perform both tests, this is the right way to do the job because Linux supports many more types of files including sockets, links and pipes. Executing fileOmdir.py generates the following kind of output:

### Using cp

The following output shows various uses of the cp utility.

```
$ ls -l /bin/cp
-rwxr-xr-x 1 root root 150824 Mar 14 2015 /bin/cp
$ cp /bin/cp .
$ ls -l cp
-rwxr-xr-x 1 mtsouk mtsouk 150824 Oct 19 22:09 cp
$ rm cp
$ cp /bin/cp /tmp/
$ ls -l cp
-rwxr-xr-x 1 mtsouk mtsouk 150824 Oct 19 22:09 cp
$ cp m /bin/cp /tmp
$ cp -i /bin/cp /tmp
cp: overwrite '/tmp/cp'? y
```

```
$ ./fileOmdir.py .
. is a directory!
$ ./fileOmdir.py /usr
/usr is a directory!
$ ./fileOmdir.py /bin/cp
/bin/cp is a file!
```

The first command copies the cp executable into the current directory – as you can see, the new file belongs to the current user, whereas the original file belongs to the root user. The last cp command illustrates the use of the -i option of cp. You can check the man page of cp() to find more information about it as well as the other supported options.

This operation is important because if the second command line argument of cp is a directory, it means that you're going to create a copy of the original file, which is given as the first command line argument, into that directory. Additionally, if the first command line argument is a directory, then the Python script won't work.

### Dealing with files

This part of the tutorial will present Python 3 methods that are related to files. It will enable you to add some extra features to pycp.py. The following Python 3 code, saved as fileOperations.py, shows some of the methods that explore file metadata:

```python
#!/usr/bin/env python3
import sys
import os
import stat
from stat import *

if len(sys.argv) >= 2:
    filename = str(sys.argv[1])
else:
    print('Not enough arguments!')
    sys.exit(0)
```

### Identifying files and directories

You'll need to find a way to differentiate between directories and regular files, which is the job of fileOmdir.py:

```python
#!/usr/bin/env python3
import os
import sys

if len(sys.argv) >= 2:
    what = str(sys.argv[1])
else:
    print('Not enough arguments!')
```

> ### Quick tip
Systems programming is a special area of coding. When UNIX was first introduced, the only way to write systems software was by using C. Nowadays you can develop systems software using other programming languages including Python, Perl, Rust and Go.
