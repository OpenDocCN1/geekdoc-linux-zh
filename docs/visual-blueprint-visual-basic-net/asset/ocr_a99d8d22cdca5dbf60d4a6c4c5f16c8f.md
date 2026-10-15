# USING VALIDATION CONTROLS

Validation controls enable you to check the values of user-entered data to ensure the values make sense. The validation controls automatically generate client-side scripts to provide this validation.

Web Forms provide a number of validation controls. The RequiredFieldValidator ensures that the user completes in an input control, such as a text box. The RangeValidator checks that a user's entry falls in a valid range of values. The CompareValidator checks the user's entry in one control against that in another control, or against a string value. For information on the regular expression validation, see the section "Work with Regular Expression Validation." To create a listing of validation errors, see the section "Provide a Validation Summary."

A validation control binds to a single input control on the form that you specify using the ControlToValidate property. The ErrorMessage property appears in the validation control when the validation fails. The Display property controls how the control shows errors. If you set Display to Static, the control uses space on the form but remains blank until an error occurs. With the Dynamic setting, the control uses no space until an error occurs, and then becomes visible. If you set the page layout for Flow, this moves elements on the page to make space for the validation control. The EnableClientScript property enables the use of JavaScript to perform the validation on the client. Otherwise, the control performs the validation using a round trip to the server.

For the CompareValidator control, you set the ControlToCompare property or the ValueToCompare property against the the text you want to compare. The Operator property specifies the comparison. The Type property specifies the variable type to use for the comparison.

For the RangeValidator control, set the MinimumValue and MaximumValue properties to the lower bound and upper bound of the acceptable entries. Use Type to specify the variable type for the comparison.

![](bbox=[0.05, 0.56, 0.95, 0.82])

+   1 Create a new Web Application project or open an existing one.
+   2 Add necessary input controls to the form and validation controls to the form.
+   3 In the Properties window, click the ControlToValidate and click the appropriate input control.
+   4 Type an error message into the ErrorMessage property.
+   5 For the CompareValidator, click ControlToCompare's and select a control or type a value for the ValueToCompare property.
+   If necessary, click the Operator and Type to select a value.

Note: See the sections "Create a Web Application" to create a new project and "Using a Web Form" to add controls.