# Chapter 4

Use the following to add data to the rest of the tables (remember you can download this code at www.wrox.comand save yourself some typing if you'd like):

```
INSERT INTO Models (model_id, model_name, make_id) VALUES (1, 'Explorer', 1), (2, 'Accord', 2), (3, 'Golf', 3), (4, 'Tacoma', 4), (5, 'Corvette', 5);
INSERT INTO New_Vehicles (model_id, modelyear, color, description) VALUES
(1, 2005, 'Dark Blue', 'Popular SUV; great for moving people or cargo across town, or wherever your adventuures may take you.'),
(NULL, 2004, 'Graphite Pearl', 'Last of the 2004 stock! Must sell! Loaded, all options!'),
(4, 2005, 'Radiant Red', 'Come drive this terrific truck! 4WD, extended cab, many options.'),
(5, 2005, 'Daytona Sunset Orange Metallic', 'All the new C6 Corvette, the next generation of classic American sportscars. 400HP V8; very fast!'),
(1, 2005, 'Dark Blue', 'Popular SUV; great for moving people or cargo across town, or wherever your adventuures may take you.');
INSERT INTO Used_Vehicles (model_id, modelyear, color, mileage, certified, warranty, description) VALUES
(1, 2000, 'White', 64800, 0, 0, 'Good condition; One owner; 4WD; V6'),
(2, 2003, 'Deep Green Pearl', 27300, 0, 1, 'Excellent condition, off-lease vehicle; Must see!'),
(3, 2004, 'Reflex Silver', 3800, 1, 1, 'R32 Limited edition; Low miles; Understated and surprisingly functional; Loaded.'),
(4, 1993, 'Red', 152000, 0, 0, 'Runs decent; 4WD; Tinted windows, aftermarket stereo; Needs a little TLC.'\);
```

Note that there is a NULLvalue for the model_id of the second vehicle you added to the New_Vehicles table. You'll find out why later on.

# Retrieving Information

You've spent all that time creating your database tables and populating them with data; now it's time to get some of that data back out. For this, you will use the SELECTstatement. A simplified form of SELECT looks something like this:

```
SELECT [column_names] FROM [table] WHERE [criteria]
```

If you wanted to retrieve a list of the colors of your used cars, for example, you would use something similar to the following:

```
SELECT color FROM Used_Vehicles;
```

which would return the following:

![](bbox=[0.12, 0.82, 0.3, 0.93])