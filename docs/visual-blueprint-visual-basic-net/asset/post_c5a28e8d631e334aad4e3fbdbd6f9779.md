
# MONITORING A WINDOWS SERVICE

You can monitor and manipulate the state of a Windows service from another application. For example, you can provide a configuration interface that allows the user to configure properties of the service. When the user makes configuration changes, you can stop and restart the service to allow configuration changes to go into effect.

The ServiceController component, part of the System.ServiceProcess namespace, manipulates running services. You can add this component via the Component section of the Toolbox, or you can create an object instance of the class in code. Two properties specify the service to use. The MachineName property sets the machine on which the service runs. You set it to a period (.) if the service runs on the local machine. You set the ServiceName property to the name of the service to manipulate.

The CanPauseAndContinue property returns a value that determines whether the service can pause and resume. If this value is True, you can use the Pause method to pause the service and the Continue method to resume execution of the service. The CanStop property returns a value that determines whether the service can stop after it starts. If you set this to True, you can stop the service with the Stop method. You can start a service using the Start method.

The Status property returns the current status of the service. The property returns a constant from the ServiceControllerStatus enumeration. If you want your application to wait for the service to reach a particular state, use the WaitForStatus method. Pass a constant from the ServiceControllerStatus enumeration as the first parameter. Optionally, you can pass a TimeSpan object as the second parameter if you want the wait to time out.

![](img/d6f772854306e15fb6df39b861a7b541_281_0.png)

![](img/d6f772854306e15fb6df39b861a7b541_281_1.png)

- 1. Create a new Windows Application project.
- 2. Click the Components section of the Toolbox and double-click the ServiceController component.
- 3. In the Properties window, type the computer name on which the service runs in the MachineName property.
- 4. Type the name of the service into the ServiceName property.
- 5. In the method of the form to manipulate the service, type the name of the component and follow it with .Stop() to stop the service.
- The example adds three buttons, using Button1 to stop the service, Button2 to start it, and Button3 to check the status.

# Extra

You can retrieve a list of the services that are currently running on a machine. You use the GetDevices method to return a list of device driver services, and the GetServices method to access a list of non-device driver services. Both methods return an array of ServiceController classes representing each of the services. To access services on the local computer, you specify no parameters to the methods. For a remote computer, specify the computer name as the only parameter. The ServicesDependedOn property returns an array of services on which the service depends. You can use the ServiceControllerStatus enumeration to examine the status of the service with the Status property.

| CONSTANT | DESCRIPTION |
|---|---|
| ContinuePending | The service is attempting to resume. |
| Paused | The service is paused. |
| PausePending | The service is moving to pause state. |
| Running | The service is running. |
| StartPending | The service is starting. |
| Stopped | The service is stopped. |
| StopPending | The service is stopping. |

![](img/d6f772854306e15fb6df39b861a7b541_282_0.png)

![](img/d6f772854306e15fb6df39b861a7b541_282_1.png)

- 6 To start the service, type the name of the component followed by .Start().
- 7 To check the status of the service, type If ServiceController1.Status = replacing ServiceController1 with the name of the service.
- 8 Type a constant from the ServiceController Status enumeration and complete the If statement.
- 9 Press F5 to run your application.

The service responds appropriately to the commands sent by the ServiceController.
