LEFT OUTER JOIN Models mo USING (model_id) LEFT OUTER JOIN Makes ma USING (make_id)) \YG

Run this and you’ll see the following:

************************* 1. row **************************

make_name: Ford
model_name: Explorer
color: Dark Blue
modelyear: 2005
price: NULL
description: Popular SUV; great for moving people or cargo across town, or wherever your adventures may take you.
NULL: NULL
1: 1

************************* 2. row **************************

make_name: NULL
model_name: NULL
color: Graphite Pearl
modelyear: 2004
price: NULL
description: Last of the 2004 stock! Must sell! Loaded, all options!
NULL: NULL
1: 1

************************* 3. row **************************

make_name: Toyota
model_name: Tacoma
color: Radiant Red
modelyear: 2005
price: NULL
description: Come drive this terrific truck! 4WD, extended cab, many options.
NULL: NULL
1: 1

************************* 4. row **************************

make_name: Chevrolet
model_name: Corvette
color: Daytona Sunset Orange Metallic
modelyear: 2005
price: NULL
description: The all new C6 Corvette, the next generation of classic American sports-cars. 400HP V8; Very fast!
NULL: NULL
1: 1

************************* 5. row **************************

make_name: Honda
model_name: Accord
color: Deep Green Pearl
modelyear: 2003
price: NULL
description: Excellent condition, off-lease vehicle; Must see!
NULL: 0
1: 1

************************* 6. row **************************

make_name: Volkswagen
model_name: Golf