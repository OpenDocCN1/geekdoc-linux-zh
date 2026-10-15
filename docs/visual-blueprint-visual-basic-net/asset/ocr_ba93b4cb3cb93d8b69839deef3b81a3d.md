# REFERENCE A LIBRARY

The Windows Control Library project builds a DLL that contains a set of UserControl controls, which you can reuse in your applications. The Class Library project also builds a DLL that normally contains components and classes that you can reuse across projects. These projects build the same library type. The template only varies in the type of component it initially provides when you create the project.

To use a library in another project, you indicate the compiled DLL library to reference in your project. Referencing a component library means that you now can access the classes, components, and controls that the library exports. The library is not part of your application, however, and you cannot access private parts of the library.

To reference a component or class library in an application, you use the Add Reference dialog box. A reference makes all of the classes in the component library available, but you cannot use the controls automatically. You must customize the Toolbox and select from the library which controls and components you want available in the Toolbox.

Each assembly resides within its own namespace. Therefore, to add a library to another application, you must remember your library project's namespace to access the components and controls inside of the library. Unless you change the root namespace of the library project, the namespace is the same as the name of the project.

Because the reference you make saves into the assembly of your application, you can create a setup project that automatically installs the appropriate component library DLL with your application.

# ADD A REFERENCE

+   1. Create a new Windows Application project or open an existing one.
+   2. Right-click the project in the Solution Explorer.
+   3. Click Add Reference.
+   4. Click Browse and select the DLL file.
+   5. Click OK.

The Add Reference dialog box appears.

The library project places the built DLL in the bin\ subdirectory of the project directory.

![](bbox=[0.04, 0.55, 0.92, 0.78])