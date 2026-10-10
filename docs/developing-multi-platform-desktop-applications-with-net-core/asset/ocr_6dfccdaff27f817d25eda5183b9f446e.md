The work around is to use dummy object or database for imitating the real data or object in interaction with the function the developer needs to unit test.

This concept is called mocking. Mocks isolate the method/function you want to test and validate if it is running on its own (independently of the other methods). Mocks can setup object with given values and set properties of this object.

The developer has to hard code attended input values for the method and define a validation test with the expected result value (hard coded too).

For .Net Core 3 development we recommend to use the Moq (4.x), this is the most popular and user-friendly mocking framework. Moq is a library that makes easy to develop and test mocks, moreover this library provide LINQ to Mocks feature allowing to dynamically request the mock objects for the validation. It supports mocking interface and class as well.

![](bbox=[0.02, 0.67, 0.08, 0.75])

+   - https://github.com/moq/moq4/
+   - https://github.com/moq/moq4/wiki/Quickstart

You can add the following package to the test project for a rapid integration of Moq.

![](bbox=[0.02, 0.89, 0.1, 0.95])

Moq

The latest version of this package is implemented with .NET Standard 2.0, so it is usable within .NET Core 3 project (that is the beauty of the .NET Standard library format).