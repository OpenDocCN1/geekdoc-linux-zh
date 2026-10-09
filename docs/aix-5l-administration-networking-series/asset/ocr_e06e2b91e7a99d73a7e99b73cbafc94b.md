machine. These logical system partitions are considered independent systems to the outside world and can be managed as independent systems. IBM allows you to create these LPARs by specifying the exact number of processors and memory for the logical system, and allows different OS (AIX and Linux) versions to run within the same machine. This is an incredible break through tool for development shops! When they need a sandbox to play in, just create one-on-the-fly.

The ODM class CuOD is responsible for the dynamic mechanisms that make some of these technologies work; of course, the POWER 4 processor is required also.

> **NOTE A POWER 4 CPU chip is really a 2-way SMP on a single chip that can be independently controlled!**

# ## A Sampling of ODM Object Classes

A special object class, predefined connections (**Pd**Cn), defines the hierarchy of device classes and subclasses. Device attributes are maintained as separate attribute object classes. See Table 9-3 for a sampling of AIX object classes.

You can display object class definitions using the **odmshow** command.

```
# odmshow <ObjectClassName>
```

Tables 9-4 through 9-7, representing the predefined and customized device and attribute descriptors, will give you some idea as to how device information is represented and linked.

| Class Object | Contents of the Object Class |
|---|---|
| PdDy | Predefined devices supported by AIX |
| PdAt | Predefined device attributes |
| PdCn | Predefined device subclass connections |
| CuDy | Customized devices attached to the system |
| CuDvDr | Customized device drivers |
| CuAt | Customized device attributes |
| CuDep | Custom device dependencies |
| CuVPD | Customized vital product data |
| Config_Rules | Configuration rule sets |

Table 9-3. Sampling of AIX Object Classes