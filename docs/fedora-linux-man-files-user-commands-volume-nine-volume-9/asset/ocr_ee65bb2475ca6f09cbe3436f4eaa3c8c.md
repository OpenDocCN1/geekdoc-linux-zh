```
```
import java.rmi.*; import java.rmi.activation.*; ActivationSystem system;
system = (ActivationSystem)
Naming.lookup("//port/java.rmi.activation.ActivationSystem");
```
```

-stop Stops the current invocation of the **rmid** command for a port specified by the **-port** option. If no port is specified, then this option stops the **rmid** invocation running on port 1098.