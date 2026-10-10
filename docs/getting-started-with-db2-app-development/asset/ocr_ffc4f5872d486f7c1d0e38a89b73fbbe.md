# 7

# Chapter 7 - Application development with Ruby on Rails

Ruby is an open source, free, dynamic programming language. Ruby on Rails (RoR), or Rails for short is a framework built using Ruby. RoR is based on the Model, View and Controller (MVC) architecture. By supporting agile development techniques it has enabled many developers to radically reduce the time and pain involved in creating Web applications.

In this chapter you will learn about:

+   - Ruby on Rails and the MVC architecture
+       - How to setup Ruby on Rails to work with DB2
+       - A basic understanding of ways to program RoR applications with DB2
+       - How to build a simple Ruby on Rails application with DB2

# ## 7.1 Ruby on Rails applications with DB2: The big picture

Ruby on Rails is organized around the Model, View, and Controller architecture, usually just called MVC. MVC benefits include:

+   - Isolation of business logic from the user interface
+   - Making it clear where different types of code belong for easier maintenance

A Model represents the information (data) of the application and the rules to manipulate that data. In the case of Rails, models are primarily used for managing the rules of interaction with a corresponding database table. In most cases, one table in your database will correspond to one model in your application. The bulk of your application’s business logic will be concentrated in the model. Under this architecture, DB2 provides data persistence.

Controllers provide the “glue” between models and views. In Rails, controllers are responsible for processing the incoming requests from the Web browser, interrogating the models for data, and passing that data on to the views for presentation.