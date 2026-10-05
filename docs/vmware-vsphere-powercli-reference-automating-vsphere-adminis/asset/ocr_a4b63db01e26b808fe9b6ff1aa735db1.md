Within the workflow presentation, set all of the inputs, except keepTogether, to Mandatory. Figure 21.23 shows an example of how to set one of these using the drsRuleName input. Select the input and the Properties tab add the Mandatory input.

# FIGURE 21.23 New-DRSRule (Presentation tab)

![](bbox=[0.318, 0.231, 0.858, 0.563])

Within the workflow schema, add a scriptable task and name it Set arguments on the Info tab. On the In tab of the task, add all of the parameters of the workflow (Figure 21.24).

On the Out tab of the task, create the following (Figure 21.25):

+   - arguments - Type: string, as workflow attribute