First, the driver builds a directed acyclic graph (DAG), which is a sort of summary of all the operations that are performed on the RDDs, like loading, map, flatMap, storing as a file, and so on (see Figure 12-1).

![](bbox=[0.21, 0.18, 0.62, 0.3])

Figure 12-1: Example of a simple DAG composed of two steps: parallelize and map

The driver then registers the workload on the master by sending a few key properties: the workload's name, the memory requested, the number of initial executors, and so forth. The master acknowledges the registration and assigns Spark workers to the incoming job. It shares their details (IP and port number) with the driver, but no action follows. Up until this point, no real computation is performed. The data still sits on the driver's side.

The driver continues parsing the script and adding steps to the DAG, when needed, until it hits what it considers to be an action, a Spark API that forces the collapse of the DAG. This action could be a call to display an output, save a file, count elements, and so on (you can find a list of Spark actions at http://bit.ly/3aW64Dh). Then and only then will the DAG be sent to the Spark workers. These workers follow the DAG to run the transformations and actions it contains.

Fine. We upgrade our code to add an action (in this case, a collect method) that will trigger the app's submission to a worker node (see Listing 12-7).

```
```python
from pyspark import SparkContext, SparkConf
--snip--
partList = sc.parallelize(range(0, 10))
Popen(["hostname"], stdout=subprocess.PIPE).stdout.read()

for a in finallist.collect():
    print(a)
```
```

Listing 12-7: Adding an action to the malicious Spark application

But we're still missing a crucial piece. Workers only follow the DAG, and the DAG only accounts for RDD resources. We need to call Python's Popen in order to execute commands on the workers, yet Popen is neither a Spark transformation like map nor an action like collect, so it will be omitted from the DAG. We need to cheat and include our command execution inside a Spark transformation (a map, for instance), as shown in Listing 12-8.

```
```python
from pyspark import SparkContext, SparkConf
from subprocess import Popen
```
```