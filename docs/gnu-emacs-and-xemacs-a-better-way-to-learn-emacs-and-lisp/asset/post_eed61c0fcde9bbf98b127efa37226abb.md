
## Chapter 8: Byte-Compiling for Efficiency
121
- The Byte-Compiler
  122
- How to Run It
  124
- Keyboard Commands
  125
  - Using the Menu
    126
- Interpreting Error Messages
  126
  - Error Types
    127
- Problems with Different Emacs Versions
  128
- Edits That Seem to Have No Effect
  129
- Conclusion
  130

## Part II: Learning to Configure Emacs with Lisp
131

## Chapter 9: First Steps in Customization: Your .emacs File
133
- This File Makes Your Editor Unique
  134
- Building Blocks of the File
  134
  - Functions
    134
  - Definitions
    134
- Troubleshooting the File
  135
  - Handling Parentheses
    135
  - Parenthesis Modes
    135
  - Other Sources of Errors
    136
  - Comments
    136
- Backing up Your .emacs File
  137
- Byte-Compiling .emacs
  137
- Splitting Your .emacs File
  138
- Loading the New Files
  139
- A Little Reassurance
  140
- Trying out the Sample Files
  140
- Copying Files from the CD-ROM...141
- Sample .emacs Files...141
  - An .emacs Optimized for HTML...141
  - A Programmer's .emacs...142
  - A LaTeX Writer's File...142
  - New Keybindings...143
  - An .emacs with Macros...143
  - A Gnus User's .emacs...143
- XEmacs, GNU Emacs, and Their .emacs Files...143
- Conclusion...144

## Chapter 10: Changing Default Behavior
145
- Puzzling Defaults...146
  - Backspace and Delete...146
  - Beeping...149
  - Syntax Highlighting...150
  - Word Wrapping...155
  - Fonts...157
- Your Own Keybindings...160
  - How Keys Can Be Represented in Lisp...161
  - Keymaps, Global and Local...161
  - Mode-Specific Bindings...164
  - Keys and the Console...164
- The Title Bar...164
- Conclusion...165

## Chapter 11: Modes, Major and Minor
167
- Introducing Modes...168
- What a Mode Does for You...169
  - Syntax Highlighting...170
  - Keybindings...171
  - Indentation...172
  - Word Wrapping...172
- **Minor Modes**...172
  - *The Advantages of Multiple Modes*...173
  - *Mode Hooks*...173
  - *How to Associate Modes*...174
  - **Different Ways to Load a Mode**...174
    - *Load*...175
    - *Autoloading*...175
    - *Require*...176
  - **Deriving One Mode from Another**...177
  - **Modifying a Mode**...179
  - **Conclusion**...180

## Part III: Exploring Emacs Packages
181

## Chapter 12: Introduction to Packages
183
- The Rationale behind Packaging...184
- **GNU Emacs Packages**...185
  - *How Packages Are Activated*...185
  - *Finding Installation Instructions*...186
  - *Installing a New Version*...188
  - *The Site-Lisp Directory*...188
- **The XEmacs Packaging System**...189
  - *A New Way to Manage Packages*...190
  - *Types of Packages*...190
  - *The Directory Structure*...190
- **Installation Methods**...191
  - *Installing Individual Packages Manually*...191
  - *Using the Menu Interface*...191
  - *Linux Distributions and XEmacs Packages*...194
- Installing a Sumo Tarball....194
- Conclusion....195

## Chapter 13: Text Processing Packages
197
- Text Processing and Word Processing....198
- When a Word Processor Is More Appropriate....199
- LaTeX, HTML, and Lout As Alternatives....200
- HTML Modes....201
  - Setting up to Write HTML....202
  - GNU Emacs' Built-in Mode....203
  - html-helper-mode....203
  - bm—html-menus....208
  - psgml and HTML....209
- LaTeX or Lout?....212
  - LaTeX....213
    - TeX, LaTeX, and Linux....214
    - A Basic TeX Mode....215
    - AUCTX....215
      - Installation....215
      - Syncing with Your TeX Installation....217
      - Menus and Keybinding....217
      - Running TeX....219
      - Viewing and Printing Your File....220
  - Lout....220
    - Installing Lout....221
    - Using lout-mode....221
    - Processing and Printing....223
- Conclusion....224

## Chapter 14: Built-in Convenience Packages
225
- Abbreviation and Expansion....226
  - abbrev-mode....226
  - Saving Abbreviations ........................ 228
  - *Dynamic Abbreviation* ........................ 228
- **Bookmarks** .................................................... 229
  - Saving and Revisiting Bookmarks ........................ 230
- **Dired, the Emacs File Manager** ............................ 233
  - *Dired Keys* ............................................. 234
  - *The Regexp Menu* ....................................... 234
  - Customizing Dired ...................................... 235
  - Dired Tips ............................................ 235
- **Differences between Files** ...................................... 236
  - *Navigation within Ediff Buffers* ............................ 238
  - *Working with Directories* ............................... 238
  - *Working with Differences* ............................... 239
  - Merging Files ........................................... 240
  - *Patching Files with Ediff* .................................. 240
  - Learning More ............................................ 241
- **Spell Checking with ispell** .................................... 241
  - ispell Commands ......................................... 242
  - *Dictionaries for ispell* ................................ 243
  - *Customizing ispell* .................................... 243
  - *Flyspell* ................................................. 244
- **Running a Shell in Emacs** ..................................... 245
  - *Shell Buffer Keybindings* ................................ 245
  - *Shell Buffer Problems* ................................ 246
  - Exshell ................................................ 247
- **Outline Mode** ................................................ 248
  - Starting Outline Mode ................................... 248
  - *Outline Levels* .......................................... 249
  - Expanding and Collapsing Outlines .................... 251
  - *Deletion and Outlines: A Warning* .................... 253
  - *Other Outline Modes* .................................. 253
- **The Calendar and the Diary** ................................ 253
  - *The Diary File* .......................................... 255
- **Conclusion** ................................................. 256

## Chapter 15: External Convenience Packages
257
- Clipper: A Persistent Clipboard ................................... 258
  - Installation ..................................................... 259
- Notes Mode ...................................................... 259
  - Prerequisites .................................................. 260
  - Installation .................................................... 260
  - Keyboard and Mouse Commands ......................... 265
- Folding Mode ...................................................... 266
  - Installation ...................................................... 267
  - Keyboard and Menu Commands ....................... 268
- An Interface to Online Dictionaries ............................. 270
  - Dictionary.el Installation ................................. 271
- Emacs CD and MP3 Players .................................... 273
  - A CD Interface ................................................. 273
  - Playing Lists of MP3s ................................... 274
- An ABC Mode for Musicians .................................. 275
  - Installation ...................................................... 276
  - Using abc-mode .............................................. 276
- The Remembrance Agent ......................................... 276
  - Unpacking and Installation ............................. 278
  - Setting up Searchable Sources ........................ 279
  - RA Commands .................................................. 280
  - License Issues .................................................. 282
- Conclusion ......................................................... 282

## Chapter 16: Packages That Make Programming Easier
283
- A Mode for Nearly Every Language ............................ 284
- Dealing with Comments ......................................... 285
- A Mode for C, C++, and Java ................................... 286
  - Navigating through Source Files ........................ 287
  - Indentation Styles .......................................... 287
