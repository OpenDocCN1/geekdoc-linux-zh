# CHAPTER 5 Designing Experiments

the dependency installation process. To facilitate this, the dependencies of each test
profile are expressed with a generic name, which is translated to the distro-
specific package name via a predefined list. For instance, a test profile might require
the generic "gtk-development" package, which will translate to "gtk2-dev" on
Fedora, "x11-libs/gtk+" and "libgtk2.0-dev" on Ubuntu. In the case where
packages must be installed but the current user not have the necessary privileges,
t user will be prompted for their root password, and then the packages will be
installed automatically. The generic package names and their corresponding package
ames for each package manager can be found in ${PTS_SRC}/pts-core-
test-dependencies/xml}.

Fourth, a directory is created for the test installation. This directory will reside
in the ${HOME}/phorix-test-suite/installed-tests directory, under
t parts, for official tests, or local, for custom tests, directories. For example,
in the official test profile unpack-linux-1.0 is installed, it will be installed into
${HOME}/phorix-test-suite/installed-tests/pts/unpack-linux-1.0.0.

Fifth, any more resources required for testing are demanded. These resources
typically include the benchmark's workloads or source code. Phoronix units
checking both the file size and checksum in order to verify each file's download
integrity. Before each file is downloaded, the download cache is searched. If the file
is found, meets the integrity requirements, the download will be skipped and the
file will be copied from the download cache. By manually copying files into the download cache, tests can be installed and run on
systems that have a network connection. If the file is not found within the download
cache, Phoronix will attempt to download it into the cache and copy it into the
t's installation directory.

Sixth, the test profile's install.sh script is executed. This script is responsible
of creating the executable, typically a script, that will set and perform the actual
benchmarking, as well as setting up any prerequisites. For example, a common
function of the installation script is to compile any downloaded code and then create
tcript that runs the benchmark.

Once this script has finished executing, the test is installed and ready to be run. If
t suite is referenced, this process will occur for every test profile contained within
t suite. If a local or OpenBenchmarking.org result is referenced, this process
will occur for every test profile within the result test.

# Running tests

Once a benchmark has been installed, it is ready to be run and for results to be col-
lected. Running individual benchmarks or test suites can be accomplished by running

```
$phorix-test-suite run <test-reference>
```

First, the Phoronix Test Suite will ensure that the selected benchmark,
or benchmarks, are installed. If not, the user will be prompted whether they wish to
install the tests or abort.