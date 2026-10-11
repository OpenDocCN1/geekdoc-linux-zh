# # 14
## Functions and Script Execution

ONCE I WAS DISCUSSING THE PROBLEM OF "PREACHER BURNOUT" WITH A MINISTER. When people train for a life in the clergy, they are expected to master not only the concepts taught by the faith, but also accounting, counseling, writing, graphic design, and a dozen other skills. Although this guarantees that the minister has a ready background in all the areas needed to keep a congregation moving forward, it also instills in many new church leaders the feeling that they must single-handedly bear the needs of the congregation, unable or unwilling to delegate responsibilities. No human being can shoulder that many duties effectively. This burden often leads to stress, feelings of helplessness, emotional breakdowns, or even the abandonment of their chosen profession.

Shell scripting is a tool for solving simple problems quickly. When scripts become large or complex, they become difficult to maintain. Like someone suffering from "preacher burnout," they must delegate responsibilities to other scripts and coordinate with each other to get jobs done without crumbling under the load.

# ## Running Scripts

Bash scripts are text files and not files containing executable instructions. A script cannot be executed directly; it needs an interpreter to carry out the instructions. In the case of Bash scripts, the interpreter is the Bash program. Linux must be able to find the interpreter in order to run a script.

One way is to run an interpreter explicitly starting a new Bash session. To run a script named _delayed_shipments.sh_, you supply the name to Bash as an argument.

```
```
$ bash delayed_shipments.sh
```
```

The alternative way requires a `#!` line as the first line of the script. This specifies the pathname of the interpreter needed to run the script. In this case, `#!/bin/bash` specifies the pathname of the Bash shell that's located in the `bin` directory. The script should have the permission bits set to allow the user to run the script. (Permission bits are discussed more in the next chapter.) The script can then run without explicitly starting Bash; Linux automatically starts Bash for you.

```
```
$ delayed_shipments.sh
```
```