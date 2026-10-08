Then, as we did before, we need to change the port, this time from 5432 to 5433, as seen in the following screenshot:

![](bbox=[0.137, 0.146, 0.862, 0.417])

Figure 13.8 – Changing the port on postgresql 12

Then, save the file with **Ctrl + O** and exit with **Ctrl + X.**

Now, we just need to restart **postgresql** with the following command:

```
sudo systemctl restart postgresql
```

This should fix the issue!

Now, we can go back and run the OpenVAS configuration script, as follows:

```
sudo gvm-setup
```

Now, after a few minutes, you should see something like this:

![](bbox=[0.137, 0.7, 0.862, 0.758])

Figure 13.9 – OpenVAS configuration and password

> Tip
Make sure you copy the password and save it in a safe location as you will need to access OpenVAS.

At this point, you are ready to start OpenVAS!