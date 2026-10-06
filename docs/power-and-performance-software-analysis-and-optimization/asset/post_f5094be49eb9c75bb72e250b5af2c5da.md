
by the merge operation. Instead, a new result is created in the default test-results directory, starting with the name merge-.

## 5.4.3 CREATING CUSTOM TESTS

Regardless of whether published or not published, adding custom tests to the default repertoire is very simple. Essentially, a test profile is a collection of XML files and executables, normally shell scripts, for performing installation and benchmarking.

First, create a new directory for the test profile in $HOME/.phoronix-test-suite/profiles/local. In this directory, all of the files needed for installing the test, except for any external resources, will be created. This XML file

The heart of a test profile is the test-definition.xml file which describes not only the metadata, such as the name and description, but also the required software, PhoronixTestSuite.TestProfile.External Dependencies for running the actual benchmark, PhoronixTestSuite.TestInformation.Executable, as well as data about the result metrics. The PhoronixTestSuite.Information.ResultScale property is the label used for the metric, such as “seconds” or “MB/s.” The PhoronixTestSuite.TestInformation.Property profile sets whether the metric is reported as “HIB” or “LIB”.

Due to the complexity of the test-definition.xml file, the author recommends simply copying from any existing test profile, and then updating or adding fields as needed. Listing 5.4 demonstrates a simple test definition.

```xml
<xml version="1.0"
<!--Phoronix Test Suite v4.4.0ml (Forsand)-->
<PhoronixTestSuite>
  <TestInformation>
    <Title>System X Decompression</Title>
    <Description>This measures the time to decompress a Linux kernel tarball using XZ.</Description>
    <ResultScale>seconds</ResultScale>
    <Proportion>LIB</Proportion>
    <TimesToRun>3</TimesToRun>
  </TestInformation>
  <TestProfile>
    <Version>1.0.2</Version>
    <SupportedPlatforms>Linux, BSD</SupportedPlatforms>
    <SoftwareType>Utility</SoftwareType>
    <TestType>Processor</TestType>
    <Maintainer>Jim Kukanas</Maintainer>
  </TestProfile>
</PhoronixTestSuite>
```

## LISTING 5.4

test-definition.xml for the system-decompress-xz test profile.

## CHAPTER 5 Designing Experiments

If the test profile depends on a specific system configuration, create a support-check.sh script. This script runs before the test is installed in order to determine whether the test is applicable to the system. A positive return value from this script indicates that the test is not applicable for the current system configuration. Listing 5.5 demonstrates a simple support check script.

```sh
#!/bin/sh
which xz
if [ $? -gt 0 ]; then
    echo "The system must provide xz for this test profile."
    echo "Some Linux distributions provided xz through the xz-utils package." > $TEST_CUSTOM_ERROR
fi
```

## Listing 5.5

support-check.sh for the system-decompress-xz test profile.

Next, the test requires any external dependencies, a download manifest is created in downloads.xml. This XML file lists the URL, filename, filesize, and MD5 checksum for each required file. At install time, these files will be fetched from the URL, validated against the file and MD5 checksum, and then copied into the test directory under $HOME/phorix-test-suite/installed-tests/. Listing 5.6 demonstrates a simple download manifest.

```xml
<?xml version="1.0"?>
<!--Phoronix Test Suite v4.0.4ml (Forsand)-->
<PhoronixTestSuite>
  <Downloads>
    <Package>
      <URL>http://www.kernel.org/pub/linux/kernel/v3.x/linux-3.7.tar.xz</URL>
      <MD5>21223369682bc44bdcfe152109583</MD5>
      <Filesize>69736096</Filesize>
    </Package>
  </Downloads>
</PhoronixTestSuite>
```

## Listing 5.6

downloads.xml for the system-decompress-xz test profile.

Next, create an install.sh script, which will carry out the actual installation of the test. Typically, this script is responsible for generating the shell script that will run the actual benchmark and redirects the results to the Phorix result parser. Listing 5.7 demonstrates a simple install script. Notice how the executable benchmarking script, system-decompress-xz, is created on line 6. All of the test output is redirected to the $LOG_FILE environmental variable. This is very important, as the only output to $LOG_FILE will be parsed for results. Also, always remember to make the script executable, as seen on line 11.

```bash
#!/bin/bash
XZ='which xz'
echo $? ~ /install-exit-status

cat > system-decompress-xz << EOT
#!/bin/sh
$XZ -dk --stdout linux-3.7.tar.xz > /dev/null 2>&1
EOT

chmod +x system-decompress-xz
```

- 5.7
install.sh for the system-decompress-xz test profile.

Additionally, if pre.sh, run.sh, or post.sh are present in the test profile, these scripts will be executed before, during, and after respectively. Finally, the last step is to define results-definition.xml. This XML file explains how Phoronix should parse results.

```xml
<?xml version="1.0"?>
<!--Phoronix Test Suite v4.4.0ml (Forsand)-->
<PhoronixTestSuite>
  <SystemMonitor>
    <Sensor>time</Sensor>
  </SystemMonitor>
</PhoronixTestSuite>
```

- 5.8
results-definition.xml for the system-decompress-xz test profile.

## 5.4 Phoronic Test Suite 97
