the Command Line” section later in this chapter. If makefile or Makefile is not used as a file name for a file containing make commands, the extension “.mk” is added as a convention.

![](bbox=[0.87, 0.08, 0.97, 0.16])

# Targets and Dependencies

Target lines indicate what can be built. They consist of a list of target files, followed by a colon (:), followed by a list of dependencies or prerequisite files.

A target file is a file that depends upon one or more prerequisite files. The prerequisite files are also referred to as dependencies. If a dependency is updated more recently than the target file, make updates the target file based on construction commands that follow the target line. The make utility will stop if an error is encountered during the construction process. A simple makefile will have the following format:

```
target:dependencies_list
construction_commands
```

The construction commands are regular commands to the shell that construct the target file, usually by compiling and/or linking. The following code shows the target line with construction commands for a file called payroll_form. Its dependencies are form.o and pay_info.o. A cc command constructs the target:

```
payroll_form:form.o payinfo.o
cc -o payroll_form form.o payinfo.o
```

A target list can contain multiple targets, but typically only one target is listed per target line. The target list cannot be empty; however the list of dependencies can be empty. Target line examples are listed below:

```
target_1:       dependency_1 dependency_2 # target with two de-pendencies
```