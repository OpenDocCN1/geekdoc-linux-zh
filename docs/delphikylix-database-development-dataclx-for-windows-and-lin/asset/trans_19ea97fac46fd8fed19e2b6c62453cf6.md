
## TColumn 标题属性

| 属性 | 描述 |
| :--- | :--- |
| Alignment | 将列标题的对齐方式设置为左对齐、居中对齐或右对齐。 |
| Caption | 指定在列标题中显示的文本。 |
| Color | 设置列标题的背景颜色。 |
| Font | 设置在列标题中显示文本的字体。 |

正如前文所述，Delphi 不会自动将数值字段的标题 `Alignment` 属性设置为 *textAlignRight*。因此，你在创建持久列时应确保检查标题的对齐方式。

## 网格选项

在设置好要在网格中显示的列之后，你可以设置网格范围选项，这些选项决定了网格的整体外观和风格。表 6.4 列出了可用的选项。

### 表 6.4 TDBGrid 选项

| 选项 | 描述 |
| :--- | :--- |
| dgEditing | 网格可编辑。用户必须按 F2 键才能开始编辑当前单元格。请注意，单个列仍可以设置为只读，这将防止在这些列中进行编辑。设置 `dgRowSelect` 选项会自动强制关闭 `dgEditing`。 |
| dgAlwaysShowEditor | 当用户通过 Tab 键进入单元格时，网格会自动进入编辑模式。用户无需按 F2 键即可开始编辑。与 `dgEditing` 类似，如果设置了 `dgRowSelect`，则 `dgAlwaysShowEditor` 会被强制关闭。 |
| dgTitles | 设置此选项时，将显示列标题。 |
| dgIndicator | 此选项强制在网格的最左侧显示一个窄列，该列显示当前记录的状态（插入、编辑或浏览模式）。 |
| dgColumnResize | 设置此选项后，允许在运行时移动或调整单个列的大小。 |
| dgColLines | 设置时，在列之间绘制垂直线。 |
| dgRowLines | 设置时，在行之间绘制水平线。 |
| dgTabs | 设置时，用户可以按 Tab 键和 Shift+Tab 键在网格中的单元格之间移动。清除时，按 Tab 键或 Shift+Tab 键将分别使焦点移动到窗体上下一个或前一个控件。 |
| dgRowSelect | 设置时，单击某行会高亮显示整行，而不是选择单个单元格。也可以通过对网格进行自定义绘制来手动实现行高亮，本章稍后会有详细说明。 |
| dgAlwaysShowSelection | 设置此选项以在网格没有焦点时也高亮显示当前单元格。 |
| dgConfirmDelete | 如果未设置网格的 `ReadOnly` 属性，此选项会在用户于网格中按下 `Ctrl+Delete` 时使 VCL 显示删除确认消息。如果未设置此选项，当用户按下 `Ctrl+Delete` 时，当前记录将被直接删除。请注意，即使未设置 `dgEditing`，`Ctrl+Delete` 也会删除当前记录。 |
| dgCancelOnExit | 此选项影响当用户离开网格时对新插入行的处理方式。设置时，未输入数据的新插入行将被取消。如果未设置，留空的插入行将被提交到数据集。 |
| dgMultiSelect | 设置时，用户可以通过按住 `Ctrl` 键并单击各个行来在网格中选择多行。 |

默认情况下，*Options* 设置为 [`dgEditing`, `dgTitles`, `dgIndicator`, `dgColumnResize`, `dgColLines`, `dgRowLines`, `dgTabs`, `dgConfirmDelete`, `dgCancelOnExit`]。我发现，当我使用 `TDBGrid` 时，我会关闭 `dgEditing` 和 `dgIndicator` 选项，并将网格的 `ReadOnly` 属性设置为 `True`。与其允许用户在网格中直接编辑，我会在他们按下 `Enter` 键时显示一个对话框，并允许他们在那里编辑当前记录的字段的值。当然，具体效果因人而异，你会在使用网格开发应用的过程中确定自己偏好的选项组合。

## 事件

除了上述列出的属性外，`TDBGrid` 还提供了一些你可以响应的事件，以便更精细地控制网格的显示和功能。这些事件列在表 6.5 中。

### 表 6.5 TDBGrid 事件

| 事件 | 描述 |
| :--- | :--- |
| OnCellClick | 当用户单击单元格时触发。当用户单击标题单元格、指示器或网格背景时不触发。 |
| OnColEnter | 焦点进入当前列后立即触发。 |
| OnColExit | 焦点离开当前列前立即触发。在此处理程序中调用 Abort 可以防止网格切换到新列。 |
| OnColumnMoved | 用户在运行时移动列后触发（但在调整列大小后不触发）。 |
| OnDrawColumnCell | 当单元格即将被绘制时触发。它用于实现自定义绘制，本章稍后会有详细说明。 |
| OnDrawDataCell | 已废弃，仅出于向后兼容性而保留。 |
| OnEditButtonClick | 当用户单击单元格中的省略号按钮时触发。 |
| OnTitleClick | 当用户单击标题单元格时发生（假设已设置 dgTitles 选项）。TClientDataSetGrid 内部使用此事件，当用户单击列标题时自动对底层数据集进行排序。 |

以下示例程序（如代码清单 6.1 所示）演示了不同的网格事件触发的时机。下一节“自定义绘制”将更详细地探讨 OnDrawColumnCell 事件。

**代码清单 6.1 Options—MainForm.pas**

```pascal
unit MainForm;

interface

uses

  SysUtils, Classes, QGraphics, QControls, QForms, QDialogs, DB, QGrids,

  DBGrids, DBClient, QExtCtrls, QStdCtrls, QDBCtrl;

type

  TfrmMain = class(TForm)

    ClientDataSet: TClientDataSet;

    DataSource1: TDataSource;

    pnlOptions: TPanel;

    pnlClient: TPanel;

    grid: TDBGrid;

    cbEditing: TCheckBox;

    cbAlwaysShowEditor: TCheckBox;

    cbTitles: TCheckBox;

    cbIndicator: TCheckBox;

    cbColumnResize: TCheckBox;
    cbColLines: TCheckBox;
    cbRowLines: TCheckBox;
    cbTabs: TCheckBox;
    cbRowSelect: TCheckBox;
    cbAlwaysShowSelection: TCheckBox;
    cbConfirmDelete: TCheckBox;
    cbCancelOnExit: TCheckBox;
    cbMultiSelect: TCheckBox;
    btnShowSelections: TButton;
    DBNavigator: TDBNavigator;

    lbEvents: TListBox;
    Label1: TLabel;
    Label2: TLabel;
    btnClearEventLog: TButton;

    procedure FormCreate(Sender: TObject);
    procedure gridCellClick(Column: TColumn);
    procedure gridColExit(Sender: TObject);
    procedure gridColEnter(Sender: TObject);
    procedure gridColumnMoved(Sender: TObject; FromIndex,
        ToIndex: Integer);
    procedure gridEditButtonClick(Sender: TObject);
    procedure cbEditingClick(Sender: TObject);
    procedure cbAlwaysShowEditorClick(Sender: TObject);
    procedure cbTitlesClick(Sender: TObject);
    procedure cbIndicatorClick(Sender: TObject);
    procedure cbColumnResizeClick(Sender: TObject);
    procedure cbColLinesClick(Sender: TObject);
    procedure cbRowLinesClick(Sender: TObject);
    procedure cbTabsClick(Sender: TObject);
    procedure cbRowSelectClick(Sender: TObject);
    procedure cbAlwaysShowSelectionClick(Sender: TObject);
    procedure cbConfirmDeleteClick(Sender: TObject);
    procedure cbCancelOnExitClick(Sender: TObject);
    procedure cbMultiSelectClick(Sender: TObject);
    procedure btnShowSelectionsClick(Sender: TObject);
    procedure btnClearEventLogClick(Sender: TObject);
    private
    procedure RetrieveOptions;
    procedure UpdateOption(Option: TDBGridOption; Active: Boolean);
    { Private declarations }
    public
    { Public declarations }
    end;

var
    TfrmMain: TfrmMain;

implementation

{$R *.xfm}

procedure TfrmMain.FormCreate(Sender: TObject);
begin
    ClientDataSet1.LoadFromFile ('C:\Employee.CDS');

    RetrieveOptions;
end;

// Options set/get methods

procedure TfrmMain.RetrieveOptions;
begin
    cbEditing.Checked := (dgEditing in grid.Options);
    cbAlwaysShowEditor.Checked := (dgAlwaysShowEditor in grid.Options);
    cbTitles.Checked := (dgTitles in grid.Options);
    cbIndicator.Checked := (dgIndicator in grid.Options);
    cbColumnResize.Checked := (dgColumnResize in grid.Options);
    cbColLines.Checked := (dgColLines in grid.Options);
    cbRowLines.Checked := (dgRowLines in grid.Options);
    cbTabs.Checked := (dgTabs in grid.Options);
    cbRowSelect.Checked := (dgRowSelect in grid.Options);
    cbAlwaysShowSelection.Checked := (dgAlwaysShowSelection in grid.Options);
    cbConfirmDelete.Checked := (dgConfirmDelete in grid.Options);
    cbCancelOnExit.Checked := (dgCancelOnExit in grid.Options);
    cbMultiSelect.Checked := (dgMultiSelect in grid.Options);
end;

procedure TfrmMain.UpdateOption (Option: TDBGridOption; Active: Boolean);
begin
    if Active then
        grid.Options := grid.Options + [Option]
    else
        grid.Options := grid.Options - [Option];

    RetrieveOptions;
end;

procedure TfrmMain.cbEditingClick (Sender: TObject);
```
