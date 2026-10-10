
## TABLE 5.6 Continued

| Character | Description |
| :--- | :--- |
| `:` | Time separator. This character is replaced with the time separator that is defined in the control panel under regional settings when it's other than `:`. |
| `/` | Date separator. This character is replaced with the date separator that is defined in the control panel under regional settings when it's other than `/`. |
| `_` | Underscore. This character inserts a space in the text. When editing a field, the cursor automatically skips over the `_` character. |
| `;` | Separator character. Used between mask, literal, and blank portions of the string. |
| `!` | If the `!` character appears anywhere in the mask, extra and optional characters are represented as leading blanks. Otherwise, extra and optional characters are represented as trailing blanks. |
| `>` | All characters following the `>` character are forced to uppercase until a `<` character is encountered. |
| `<` | All characters following the `<` character are forced to lowercase until a `>` character is encountered. |
| `<>` | All characters are accepted in whatever case the user enters them. |
| `\\` | Literal. The character following the `\` character is inserted in the string, literally, and is not interpreted as a mask character. |

> **Note**
>
> Each character in the mask represents one byte in the string—not one character. For that reason, when working with multibyte character sets, each character in the string is represented by two characters in the EditMask. For example, AA and LL each represent a single multibyte character. When inserting a literal into a mask, only single-byte literal characters can be entered.

Table 5.7 lists some examples of EditMask settings.

## TABLE 5.7 EditMask Settings

| Stored Value | EditMask | Displayed Value | Remarks |
| :--- | :--- | :--- | :--- |
| 5615551212 | `(000), 000-0000` | (561) 555-1212 | Phone number. Formatting characters are not stored. |
| 123-456-7890 | `000-000-0000;1;_` | 123-456-7890 | Social Security number. Formatting characters (hyphens) are stored. |
| 33467-0708 | `00000 -0000;1;_` | 33467-0708 | ZIP code. Hyphen is stored. |
| 5/28/01 | `199/99/00;1;_` | 5/28/01 | Date. Slashes are stored. Extra spaces are stored at the beginning of the string rather than at the end. |

![](img/fe651f295b5f960d5463c4fb581d2281_223_0.png)

The built-in Delphi edit masks leave something to be desired if you’re wanting to use anything more than a simple edit mask. The standard data-aware components don’t validate complex masks well (such as phone numbers, Social Security numbers, and the like). For this reason, you might want to consider a third-party library to assist you with data entry and validation. I use Orpheus, from TurboPower Software Company. You can find TurboPower’s Web site at `http://www.turbopower.com`.

## Simple Data-Aware Components

Most data-aware components fall into a category that I’ve defined as *simple* data-aware components. For purposes of this discussion, a simple data-aware component is one that links to a single field in a single record of a single dataset. For instance, a component that enables you to display and edit values for the `FirstName` field of a dataset is a simple data-aware component.

This contrasts with more complex data-aware components; which either display multiple values from the same dataset (such as `TDBGrid`), or which look up information from one dataset for inclusion in another dataset (such as `TDBLookupCombo` and `TDBLookupListBox`).

In this section, I’ll discuss the simple data-aware components, and following sections will cover some that are more complex. Don’t be too concerned at this point with the mechanics of creating data-aware components. Near the end of this chapter, I’ll show you how to take a non-data-aware component and create a data-aware descendent from it.

## TDBText

`TDBText` is the simplest of all the data-aware components. It is a display-only component, similar to the standard `TLabel`. To use it, drop a `TDBText` component on a form, and set the `DataSource` and `DataField` properties. The data is displayed according to the output format discussed in the preceding section.

## TDBEdit

`TDBEdit` corresponds to the standard `TEdit` component. It’s used to display and edit numeric, string, or data/time data contained in a dataset.

Data is displayed according to the underlying field’s `DisplayFormat` or `EditMask` property, and is edited according to the `EditFormat` or `EditMask` property (depending on the field type).

## TDBMemo

`TDBMemo` is similar in concept to `TDBEdit`, except that it can display and edit multiline text fields, such as unformatted notes. A `TDBMemo` is usually connected to a CLOB (Character Large Object) field, although you can also use it to edit string fields.

## TDBCheckBox

`TDBCheckBox` is used like a standard `TCheckBox`—to display and enter yes/no or true/false values. `TDBCheckBox` can be connected to a Logical or a Yes/No field in desktop databases, such as Paradox or Access. Most SQL databases, however, don’t directly support these field types. In these cases, you connect the `TDBCheckBox` to a string field, which is frequently a single character.

To define the relationship between checked/unchecked and the underlying field data, you set the component’s `ValueChecked` and `ValueUnchecked` properties. `ValueChecked` refers to the value of the field when the checkbox is marked. `ValueUnchecked` determines the value of the field when the checkbox is not marked. When the form containing the `TDBCheckBox` is first displayed, and the underlying field contains a value that does not equal either of these two properties, the checkbox is initially grayed out.

By default, the values of these two properties are true and false, respectively. In my own applications, I use a single character field (`VARCHAR(1)`) for Boolean field types. I use T for true and F for false. Because of this, whenever I drop a `TDBCheckBox` on a form, I set `ValueChecked` to T and `ValueUnchecked` to F.

### Note

If you decide to always use a single character field for Boolean field types, you might want to consider creating a simple component derived from `TDBCheckBox` that sets `ValueChecked` to T and `ValueUnchecked` to F (by default). That way, you don’t have to manually set these properties every time you use the component.

In addition, you should probably consider creating a domain in the database to specify character fields. This is the domain that I create for my own InterBase databases:

```sql
CREATE DOMAIN DOM_BOOLEAN AS VARCHAR(1)
DEFAULT 'F' NOT NULL CHECK (VALUE IN ('F', 'T'));
```

## TDBRadioGroup

`TDBRadioGroup` is used in cases where you want the user to select one option from a short list of options. By default, the value of the selected item is stored in the underlying dataset field, which means you typically connect the `TDBRadioGroup` component to a string field.

In my applications, I've found that I most often want to store the index of the selected item in an `Integer` field. This is straightforward to accomplish if you make use of the component's `Values` property. `Values` is a string list that corresponds to the `Items` property in the following manner:

- If `Values` is empty, the strings contained in the `Items` property are stored in the underlying dataset.
- If `Values` is not empty, it should contain the same number of string values as the `Items` property. When an item is selected in the radio group, the corresponding value in the `Values` property is stored in the dataset.

Using the second rule, you can store a sequential list of numbers in the `Values` property and connect the component to an `Integer` field. Delphi is then smart enough to store the numeric representation of the selected item in a dataset. In my applications, this is often a severe limitation, so I've created a descendent component named `TETHComboBox` that supports assigning a value to each string contained in the `Items` property.

![](img/fe651f295b5f960d5463c4fb581d2281_225_0.png)

**Figure 5.2**
Relationship between TDBRadioGroup's Items and Values properties.

## TDBComboBox

`TDBComboBox` works similarly to `TDBRadioGroup` because it enables the user to select an item from a list and store it in a dataset. Unfortunately, it doesn't support the `Values` property, so you can't use it to store the index of the selected item in a dataset. In my applications, this is often a severe limitation, so I've created a descendent component named `TETHComboBox` that supports assigning a value to each string contained in the `Items` property.
