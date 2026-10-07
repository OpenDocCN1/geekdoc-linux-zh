# Chapter 12 = Peripheral Device Controller Driver

![](bbox=[0.079, 0.098, 0.811, 0.253])

**Figure 12.2**
The typical control flow of the PDC driver.

with the platform framework when the gadget module is loaded and performing proper exit by releasing the resources allocated during initialization. Remember that the platform registration is specific to the way the device controller is interfaced with the platform hardware. Once the platform registration is successful, the PDC driver is responsible for setting up the device hardware and handling the interrupts. The PDC driver also provides routines to manage the USB controller power and other hardware features.

Figure 12.2 illustrates the typical control flow of the PDC driver. The first step is to initialize platform driver callbacks and then register the driver to the platform driver framework. The driver’s probe method is called when the device is connected to the platform. The probe method confirms the device and registers it to the kernel. Once the device is successfully registered, it is ready to handle USB activity.

The probe function does the major work of the PDC driver. Figure 12.3 dissects the probe method and represents its control flow. The first step in the probe method is to allocate required banks. After successful allocation of memory, you perform an ioremap that the bus memory is accessible in central processing unit (CPU) space. The next step in the probe method is to map the interrupt of the USB controller to the device controller driver. The `request_irq` function helps attach the interrupt handler to the USB controller interrupt. After registration of the interrupt routines, the probe sets up the different endpoints and buffer sizes of the device controller and passes them to the upper gadget driver. The setup includes initializing USB Request Block (URB) queues.