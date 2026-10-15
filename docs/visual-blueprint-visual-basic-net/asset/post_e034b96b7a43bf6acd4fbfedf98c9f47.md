
## USING VALIDATION CONTROLS

Validation controls enable you to check the values of user-entered data to ensure the values make sense. The validation controls automatically generate client-side scripts to provide this validation.

Web Forms provide a number of validation controls. The RequiredFieldValidator ensures that the user completes in an input control, such as a text box. The RangeValidator checks that a user's entry falls in a valid range of values. The CompareValidator checks the user's entry in one control against that in another control, or against a string value. For information on the regular expression validation, see the section "Work with Regular Expression Validation." To create a listing of validation errors, see the section "Provide a Validation Summary."

A validation control binds to a single input control on the form that you specify using the ControlToValidate property. The ErrorMessage property appears in the validation control when the validation fails. The Display property controls how the control shows errors. If you set Display to Static, the control uses space on the form but remains blank until an error occurs. With the Dynamic setting, the control uses no space until an error occurs, and then becomes visible. If you set the page layout for Flow, this moves elements on the page to make space for the validation control. The EnableClientScript property enables the use of JavaScript to perform the validation on the client. Otherwise, the control performs the validation using a round trip to the server.

For the CompareValidator control, you set the ControlToCompare property or the ValueToCompare property against the the text you want to compare. The Operator property specifies the comparison. The Type property specifies the variable type to use for the comparison.

For the RangeValidator control, set the MinimumValue and MaximumValue properties to the lower bound and upper bound of the acceptable entries. Use Type to specify the variable type for the comparison.

![](img/d6f772854306e15fb6df39b861a7b541_259_0.png)

- 1 Create a new Web Application project or open an existing one.
- 2 Add necessary input controls to the form and validation controls to the form.
- 3 In the Properties window, click the ControlToValidate and click the appropriate input control.
- 4 Type an error message into the ErrorMessage property.
- 5 For the CompareValidator, click ControlToCompare's and select a control or type a value for the ValueToCompare property.
- If necessary, click the Operator and Type to select a value.

Note: See the sections "Create a Web Application" to create a new project and "Using a Web Form" to add controls.

## Extra

Each of the validation controls, except for the RequiredFieldValidator control, accepts a blank entry without causing a validator error. In the input controls you validate, you may want to perform a test using a RangeValidator or RegularExpressionValidator control but do not want the user to leave the input control blank. For example, a RangeValidator control accepts a blank value even if the range for the validation is from 10 to 100. You can require the user to provide an entry for the input control and then validate the entry by adding a RequiredFieldValidator along with the RangeValidator, RegularExpressionValidator, or other validation control. You then specify the same input control in the ControlToValidate property for each validation control. You can customize the error message appropriately for each validation control using the individual ErrorMessage properties of the two validation controls. To conserve space for the use of two different validation controls relating to a single control, you can add a validation summary control. For more information on the ValidationSummary control, see the section "Provide a Validation Summary."

![](img/d6f772854306e15fb6df39b861a7b541_260_0.png)

![](img/d6f772854306e15fb6df39b861a7b541_260_1.png)

- 6 For the RangeValidator control, set the MinimumValue and MaximumValue properties.
- If necessary, click the Type and select a value.
- You can repeat steps 2 through 6 as necessary.
- 7 Press F5 to run your project.

The validation controls validate the data in the input controls appropriately.
