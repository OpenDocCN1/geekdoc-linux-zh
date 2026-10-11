![](bbox=[0.33, 0.09, 0.67, 0.11])

# Gitlab CI/CD

The open-source self-host solution for the control version of **Gitlab** includes a built-in **CI/CD** tool, which allows to create *Pipelines* to structure the workflow. A pipeline has the following two main components:

+   - **Jobs**: defines what to do. For example, to compile a code.
+   - **Stages**: defines when to run the jobs. For example, run a test after the code is compiled.

*Figure 13.56* shows an example workflow related to **Continuous Integration** and **Continuous Delivery**.

![](bbox=[0.15, 0.35, 0.85, 0.7])

The **Pipelines** are defined in *YAML* format, and they are defined at the project level. In the left menu of the **GitLab** portal, it allows you to define the workflow. *Figure 13.57* shows the left menu options related to **CI/CD**: