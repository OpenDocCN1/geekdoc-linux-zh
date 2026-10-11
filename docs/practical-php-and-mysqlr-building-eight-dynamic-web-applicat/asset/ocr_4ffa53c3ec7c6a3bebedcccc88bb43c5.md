In this project, you use Ajax to refresh a specific part of the calendar sidebar—preventing the need to refresh the entire screen. This makes the application feel smoother and allows you to flex your Ajax muscles.

# ## How Ajax Works

Before discussing how to actually implement an Ajax application, it’s helpful to take a minute to understand how Ajax works at a conceptual level. This is best explained with a diagram, as shown in Figure 8-4.

![](bbox=[0.08, 0.3, 0.92, 0.62])

Five distinct steps typically occur in Ajax requests. To demonstrate this, the following list describes how Ajax is applied when the user clicks an event in the calendar:

+   1. The user clicks an event in which he is interested. Instead of the link connecting to another HTML or PHP page, it triggers a JavaScript function.
+   2. The JavaScript function connects to a script that can handle the request. The function also requests that it be notified as soon as that request is answered (it does this by *registering a handler* to the response).
+   3. The PHP script that handles the request processes it and connects to the database to get the required information about the specified event.
+   4. When the script has gathered the event information, it responds to the JavaScript handler registered in Step 2. This handler—which now contains