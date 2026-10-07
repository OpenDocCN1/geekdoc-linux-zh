# # Chapter 8: Using Emacs

| Program | Editor | Settings | Desktop | emacs3@ey.email.net | 11:34:52 AM |
|---|---|---|---|---|---||
| emacs-frame@email.net | | | | | |

+   - Buffers Files Icons Edit Search Mode SGML Modify Markup View DTD Help
- Introduction to (C-h)
- Set face of parsed mask (Yes) (C-c) allow easy management of
- Live Element Indicator (Yes)
- Auto Restart DTD (Yes) natures:
- Tag Region If Active (Yes) List Valid Tags
- Normalize Trees (Yes) Show/Hide Warning Log (C-c) emission
- Balanced Tag Edit (Yes) (C-c) validation
- File Options
- User Options Submit Bug Report
- Omitting Transparent (No)
- Leave Point After Insert (No)
- Inserting Element Comment (Yes)
- Insert End On Tag Menu (No)
- Warn About Undefined Elements (Yes)
- Warn About Undefined Entities (Yes)
- Ignore Undefined Elements (No)
- Recompile DTD When Edit (No)
- Default Language Mode (No)
- Declaration (-)
- Validate Command (...)
- Markup Menu
- System Identifiers Are Preferred (No)
- Trace Entry Lookup (No)
- Public Map (...) (No)
- Catalog Files (...)
- Ecat Files (...)
- General Insert Case | ( (No)

```
```
CHAPTER/DOC(1)==-L1--All
```
```

Figure 8.15 The SGML menu in Emacs PGML mode

SGML menu, and the other PGML menus, are not associated with hot keys but have to be accessed via the menus.

# ## The Modify Menu

The Modify Menu in PGML mode allows the user to expand elements and references to make character references and various other changes to elements and their attributes (see Figure 8.17).

# ## The Markup Menu

The menu that will probably be most of use while you are editing DocBook is the Markup menu available under PGML mode (see Figure 8.17). The Markup menu allows you to insert elements and their end tags automatically, depending on tags are valid at that point in the document. This saves a lot of time and trouble when you get in the habit of using it.

To end the current element, use the command C-c / , which should be easy to remember because all end tags use the / character.

The Markup menu also gives users the ability to insert attributes in their tags.