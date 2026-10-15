# AN INTRODUCTION TO COMPONENT CREATION

Visual Basic .NET enables you to create components that you can use and reuse throughout your Windows, console, Web, and service applications.

> Components are classes that work more effectively as design tools in application development.

# Ease of Use

You can easily create your own components in code or assemble them from the existing components in the .NET Framework classes, using either Visual Basic .NET or C#. You can use non-visual components and associated features to easily incorporate resources such as message queues, event logs, and performance counters into your applications.

The .NET Framework classes greatly expand the component programming capabilities of Visual Studio .NET. Instead of a limited set of base classes, you have a large library of sophisticated components that you can use to assemble applications, or to derive high-quality components of your own.

# Component Visual Development

The new rapid application development, or RAD, support makes authoring controls and non-visual components as easy as creating forms. You start with

inheriting from an existing component, and add other components to build in the functionality you need.

# COMPONENT TYPES

You can build components that service a variety of purposes based on the needs of a particular project, or for reuse throughout multiple projects. All the components support working within the visual designer of the Development Studio, enabling you to use drag and drop to add components to your projects and to modify properties visually with the Properties window.

You can also create a specialized type of components known as controls. You can create controls that offer functionality to a form just like the controls provided by the .NET Framework. You can create both Windows and Web controls that offer their own visual interface and allow you to drag and drop them onto their respective forms.

# CREATE A COMPONENT CLASS

Components are a new idea in VB .NET. A basic component lets you create an object very similar to a class, which adds support for the designer. Standard components work in all types of applications, including console applications where no visual interface is available.

more easily than a typical class. You can modify the properties of the component visually instead of setting up a class in code. For example, you can easily add the Timer control to a form or any other application type and modify its properties in the Properties window, but the Timer itself provides no graphical interface.

You can use components to create objects that offer important functionality to forms, which you manipulate

# Project Type

You can add a component to a class library or a Windows Control Library project. You can then build this library and reference it in applications that need to use the component. For information on adding references, see the section "Reference a Library."

# Component Base

You create components by inheriting from the System.ComponentModel.Component class or implementing the IComponent interface. For more information, see the section "Create a Component."