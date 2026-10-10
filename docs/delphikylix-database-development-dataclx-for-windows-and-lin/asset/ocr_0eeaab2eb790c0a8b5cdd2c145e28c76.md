That's enough fields for this dataset. In the next section, I'll show you how to create a calculated field.

# Calculated Fields

Calculated fields, as indicated previously, don't take up any physical space in the dataset. Instead, they are calculated on-the-fly from other data stored in the dataset. For example, you might create a calculated field that adds the values of two data fields together. In this section, we'll create two calculated fields: one standard and one internal.

> **NOTE**
> 
> Actually, internal calculated fields do take up space in the dataset, just like a standard data field. For that reason, you can create indexes on them like you would on a data field. Indexes are discussed later in this chapter.

# Standard Calculated Fields

In this section, we'll create a calculated field that computes an annual bonus, which we'll assume to be five percent of an employee's salary.

To create a standard calculated field, open the New Field dialog (as you did in the preceding section). Enter a Name of Bonus and a Type of Currency.

In the Field Type radio group, select Calculated. This instructs Delphi to create a calculated field, rather than a data field. Click OK.

That's all you need to do to create a calculated field. Now, let's look at internal calculated fields.

# Internal Calculated Fields

Creating an internal calculated field is almost identical to creating a standard calculated field. The only difference is that you select InternalCalc as the Field Type in the New Field dialog, instead of Calculated.

Another difference between the two types of calculated fields is that standard calculated fields are calculated on-the-fly every time their value is required, but internal calculated fields are calculated once and their value is stored in RAM. (Of course, internal calculated fields recalculate automatically if the underlying fields that they are calculated from change.)

The dataset's AutoCalcFields property determines exactly when calculated fields are recomputed. If AutoCalcFields is True (the default value), calculated fields are computed when the dataset is opened, when the dataset enters edit mode, and whenever focus in a form moves