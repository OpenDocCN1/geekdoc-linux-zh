
## CONTENTS

### 2 dbExpress Datasets
- What Are dbExpress Datasets? . . . . . 58
- dbExpress Datasets Are Unidirectional . . . . . 58
- dbExpress Datasets Are Read-Only . . . . . 59
- dbExpress Datasets Are Lightweight . . . . . 59

- Types of Datasets . . . . . 59
  - Tables . . . . . 59
  - Queries . . . . . 60
  - Stored Procedures . . . . . 60
  - General-Purpose Datasets . . . . . 60

- Data Manipulation . . . . . 63
  - Opening a Dataset . . . . . 63
  - Closing a Dataset . . . . . 64
  - Retrieving Field Contents from a Dataset . . . . . 64
  - Navigating a Dataset . . . . . 65

- BLOB Support . . . . . 69
- Parameterized Queries . . . . . 71
- Ordering Data Returned from the Server . . . . . 73
  - Ordering Data from a Table . . . . . 73
  - Ordering Data from a Query . . . . . 74
- Master/Detail Relationships . . . . . 74
- Retrieving Schema Information . . . . . 79
- Summary . . . . . 91

### 3 Client Dataset Basics
- What Is a Client Dataset? . . . . . 94
- Advantages and Disadvantages of Client Datasets . . . . . 94
- Creating Client Datasets . . . . . 95
  - Creating a Client Dataset at Design-Time . . . . . 96
  - Creating a Client Dataset at Runtime . . . . . 101

- Accessing Fields . . . . . 103
- Populating and Manipulating Client Datasets . . . . . 105
  - Populating Manually . . . . . 105
  - Populating from Another Dataset . . . . . 106
  - Populating from a File or Stream: Persisting Client Datasets . . . . . 106
- Example: Creating, Populating, and Manipulating a Client Dataset . . . . . 108

- Navigating Client Datasets . . . . . 113
  - Sequential Navigation . . . . . 113
  - Random-Access Navigation . . . . . 114
- Client Dataset Indexes . . . . . 118
  - Creating Indexes . . . . . 119
  - Using Indexes . . . . . 121
  - Retrieving Index Information . . . . . 122

- Filters and Ranges . . . . . 126
  - Ranges . . . . . 126
  - Filters . . . . . 127
- Searching . . . . . 136
  - Nonindexed Search Techniques . . . . . 136
  - Indexed Search Techniques . . . . . 138
- Summary . . . . . 145

### 4 Advanced Client Dataset Operations
- Dataset Events . . . . . 148
- Disabling Data-Aware Components . . . . . 158
- BLOBs . . . . . 162
  - Notes . . . . . 162
  - Images . . . . . 162
  - Streamed Data . . . . . 165
  - Streamed Components . . . . . 167
  - File BLOBs . . . . . 168
  - Limitations of BLOB Fields . . . . . 168
- Nested Datasets . . . . . 172
- Undo Support . . . . . 176
  - Cancel . . . . . 177
  - The Change Log . . . . . 177
  - Viewing the Change Log . . . . . 182
- Cloning Data from Another Client Dataset . . . . . 186
- Maintained Aggregates . . . . . 192
  - Creating a Maintained Aggregate at Design Time . . . . . 193
  - Creating a Maintained Aggregate at Runtime . . . . . 195
  - Aggregate Expressions . . . . . 195
  - Aggregates Across a Group of Records . . . . . 196
  - Enabling and Disabling Aggregates . . . . . 197
  - GetGroupState . . . . . 197
- Miscellaneous Properties . . . . . 197
  - Constraints . . . . . 197
  - DisableStringTrim . . . . . 198
  - ReadOnly . . . . . 199
- Summary . . . . . 199

### 5 Data-Aware Components
- What Are Data-Aware Components? . . . . . 202
- TDataSource . . . . . 204
- Common Data-Aware Component Characteristics . . . . . 205
- Modifying Component Data from Code . . . . . 205
- Controlling When the User Is Allowed to Edit Data . . . . . 206
- Formatting and Editing Field Values . . . . . 206
- Simple Data-Aware Components . . . . . 211
  - TDBText . . . . . 211
  - TDBEdit . . . . . 212
  - TDBMemo . . . . . 212
  - TDBCheckBox . . . . . 212
  - TDBRadioGroup . . . . . 213
  - TDBComboBox . . . . . 213
  - TDBListBox . . . . . 218
  - TDBImage . . . . . 221
- VCL-Only Data-Aware Controls . . . . . 222
- Lookup Data-Aware Controls . . . . . 222
  - TDBNavigator . . . . . 223
- Creating Your Own Data-Aware Components . . . . . 225
  - TFieldDataLink . . . . . 225
  - Setting Up the TFieldDataLink . . . . . 226
  - Setting Up a Connection to the Data Source . . . . . 227
  - Responding to Changes in the Dataset . . . . . 227
  - Updating the Dataset . . . . . 227
  - Message Handlers . . . . . 228
  - Action Handlers . . . . . 228
  - Data-Aware TDateTimePicker . . . . . 228
  - Sample Application . . . . . 232
- Summary . . . . . 236

### 6 Data-Aware Grids
- TDBGrid . . . . . 240
  - TDBGrid Basic Operation . . . . . 240
  - Customizing Columns . . . . . 241
  - Grid Options . . . . . 244
  - Events . . . . . 245
  - Custom Drawing . . . . . 252
  - Solutions to Common Grid Questions . . . . . 257
  - Limitations . . . . . 263
- TClientDataSetGrid . . . . . 263
  - Automatic Sorting . . . . . 264
  - Column Customization . . . . . 265
- TDBCtrlGrid . . . . . 266
  - Properties . . . . . 267
  - Events . . . . . 267
- Third-Party Data-Aware Grids . . . . . 271
- Summary . . . . . 272
