
## Create a Windows Installer

When you complete a project, you then need to package the application for distribution. Visual Studio provides tools to develop a setup application for components, applications, and Web projects you create. You can use the tool to build a professional and customized installation program.

The Setup Wizard project enables you to create a project that supports the installation of Windows Application projects, Web Application projects, and component projects. When you add the project to a solution that contains Windows Application and component library projects, a wizard lets you select details for the installation, and then builds a project.

You can also specify for the installation to build a CAB file, which you can provide for download on the Internet. For a Windows machine, the setup project builds a single file with a .msi extension that installs using the Windows Installer tool included with recent versions of Windows and Internet Explorer.

With projects that install using the Setup Wizard, the wizard detects dependencies necessary for the project to run. For example, if the project requires database support, the setup project automatically includes a database distributable component.

Also included in every project is the .NET redistributable component. After selecting a project, the Setup Wizard asks you which parts of the application you want to distribute. The Primary output selection includes the EXE or DLL file your project outputs. The Localized resource selection includes any resource files you include in your project. You can also include source code and content files associated with the project through the wizard.

After you create the project, you can modify installation details by loading the client file system window and by specifying where files load on the client system. For more information on customizing the installation, see the section “Customize Your Installation.”

## Create a Windows Installer

![](img/d6f772854306e15fb6df39b861a7b541_325_0.png)

![](img/d6f772854306e15fb6df39b861a7b541_325_1.png)

1. Open an existing Windows Application project and call up the New Project dialog box.
2. Click Setup and Deployment Projects and then select the Setup Wizard template.
3. Type a name for the setup project.
4. Click to add the project to the current solution.
5. Click OK.

   The first Setup Wizard page appears, explaining the process.

6. Click Next to move to the second Setup Wizard page.
7. Click the appropriate setup program style.
8. Click Next.

### Extra

You can create a Windows installation program to deploy a Web application onto new servers much like installing a Windows application. When the Setup Wizard begins, you click the Create a setup for a Web application option. Before creating the setup, you must have a Web Forms project open. Then add the setup project to the solution, just like you did an installer for Windows applications in the Introduction. When you run the setup, instead of prompting you for an installation directory, like a Windows application setup, the Web application setup asks for a virtual directory on a local copy of IIS into which it installs the Web application. The setup includes all of the necessary .NET Framework files in case the Web server does not have ASP.NET installed. The File System window contains the same options, although the default folders include only the Global Assembly Cache and the Web Application Folder. The Web Application Folder item represents the Web server directory into which the Web application installs. Deploy the server by running the MSI setup file on the server that needs to run the application.

![](img/d6f772854306e15fb6df39b861a7b541_326_0.png)

9. Click items from the project to include in the setup.
10. Click Next.
11. On the fourth screen, select any files necessary to include with the setup.
12. Click Next.
13. Click Finish to complete the wizard.

   The setup project adds to the current solution.

> *Note: See “Customize Your Installation” to customize and build the setup program.*
