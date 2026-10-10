With this command the application is executed in a classical desktop application window (not in the browser, but this is still a web application).

# 8.3.5 Electron.NET application example

As Electron.NET is a popular wrapper around Electron, you will find plenty of code examples (check GitHub) for helping and guiding you for the development of your Electron.NET application (see reference links).

These examples make often an intensive use of the SPA (Single Page Application) techniques and use specialized JavaScript frameworks like Vue.JS or React... The reason is that the desktop application experience requires a minimum of blinking screen for being likely by the user and looked as a tangible desktop application.

So, the development of an application with Electron.NET implies an intensive use of JavaScript for making the buffer between the web development back-end and the desktop Front-End (who have a natural tendency to blink as a common web application).

The Electron.NET, ASP.NET Core example application we will review is the “ElectronNET-API-Demos” application from the Electron.NET repository.

This is the application of reference for this type of application. That illustrates the use of many Electron.NET features. Most of the source code is exposed in the application itself for teaching purpose.

In this sample, you will find a couple of useful techniques specific to the Electron.NET application type, these techniques can be reused in