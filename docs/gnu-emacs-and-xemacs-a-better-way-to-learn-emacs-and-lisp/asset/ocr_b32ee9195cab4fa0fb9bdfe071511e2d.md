The K&R style of indentation can cause problems with function argument declarations, because this style has them beginning in the first column. Indenting argument lists one space greatly speeds up cc-mode parsing.

See the cc-mode Info files for more on this topic.

# ## cc-mode and Java

cc-mode can be used to edit Java code. It knows about Java syntax, commenting, and indentation, but an extension built on top of cc-mode is preferable. It's called the JDE, which stands for Java Development Environment. Read all about it in the next section.

# ## JDE

The Java Development Environment is one of the "big modes"; it's large and complex, but it comes with well-illustrated HTML documentation. I can only scratch the surface in this chapter's coverage of the mode, but hopefully this section will be enough to pique your interest and get you off to a good start with JDE.

JDE, like many free software projects, began with a single developer. Paul Kuncean started the project and is still the maintainer, but in recent years a sizable user community has arisen, complete with an active mailing list and many user contributions.

# ## Requirements and Installation

You can use any Java Development Kit with JDE, but it will need some customization to be used with kits other than one of the official JDKs from Sun Microsystems. See the later section "Customizing JDE" for details.

# ## GNU Emacs Installation

A GNU Emacs JDE installation requires several external Emacs packages:

+   - semantic
+   - beanshell
+   - elib
+   - eieio
+   - Speedbar

The Speedbar package is included with GNU Emacs, but it is a good idea to install a newer version in order to make it work with the other required packages.