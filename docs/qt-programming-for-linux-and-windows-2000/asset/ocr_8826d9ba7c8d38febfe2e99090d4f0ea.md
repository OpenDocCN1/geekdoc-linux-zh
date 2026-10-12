where the defect is *detected* within the source code. The point where the error actually occurs will require inspection of the code. You may need to set breakpoints and step through the code's execution, but that is seldom necessary and usually time-consuming.

Intermittent defects require a great deal more work and require a very clear problem description. You will have to analyze every line in the code that can possibly result in the reported behavior. You may find other defects that haven't been reported during this process, so don't consider the time completely wasted.

# RAPID APPLICATION DEVELOPMENT

Face it: Creating large, complicated dialog screens is a tedious chore, no matter what platform you're developing for or what toolkit you're using to get the job done. Qt is no exception. While a future Qt product may include a "what you see is what you get" (WYSIWYG) dialog editor and code generator, the current releases don't. All the same, there are several useable RAD utilities available from developers that have been kind enough to make their work available to the public. The following pages describe their current feature sets and all are available via links from the Troll Web site at www.troll-tech.com.

While Troll does not currently provide a WYSIWYG builder, it is likely that they'll include one in some future release. You shouldn't let that discourage you from creating your own or modifying one of the editors mentioned below to suit your needs. The following are just a few of the IDEs and WYSIWYG editors available for Qt.

# Qt Architect

This is my favorite, just because it's the one I began working with first and because it does most of the things I needed such a tool to do (and there is a binary for Windows). Your mileage may vary. As of this writing, Qt Architect supports most of the functionality of Qt version 2.0.2, so no native support is available for the QCanvas or QDialog widgets—although you can add native support using Qt Architect's Widget Modules feature. The Qt Architect authors are very good at updating the software and seem dedicated to making a comprehensive product. It's reasonable to assume that in the time it takes to read this far in this book, the authors will have a version ready for Qt 2.1 functionality.

Qt Architect supports both layout and hard-coded geometry for widgets that are added to a dialog. Multiple dialogs can be edited simultaneously and grouped together in project-fashion. Each dialog is created as a separate set of files for the dialog parameters and source code. The dialog project files are saved as XML. (See Fig. 7.1.1.)

# QtEZ

QtEZ is more of a complete IDE than Qt Architect, but is reliant on KDE development tools and libraries, making a port to the Windows platform difficult.