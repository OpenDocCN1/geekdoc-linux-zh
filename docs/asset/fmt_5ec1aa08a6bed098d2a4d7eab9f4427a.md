
```cpp
// DialogProc 函数是与 CreateDialog 调用的应用程序定义的回调函数。
// 它处理发送给对话框的消息。
// DLPROC 类型定义了指向此回调函数的指针。
// DialogProc 是应用程序定义的名称。
BOOL APIENTRY DialogProc(HWND hDlg, unsigned iMessage, WORD wParam, LONG lParam)
{
int x;
LRESULT current;
switch (iMessage) {

// WM_INITDIALOG 消息在对话框显示之前发送。
// 对话框过程使用此消息初始化控件并执行影响对话框外观的任务。
case WM_INITDIALOG :
// CheckRadioButton 函数为指定的单选按钮添加标记，并移除组内其他单选按钮的标记。
// 如果 DialogWindow.rc 作为文本文件打开，可以找到以下行：

GROUPBOX "选择任务",IDC_STATIC,5,5,100,55
CONTROL "毁灭行星",IDC_DESTROY_PLANET,"Button",
BS_AUTORADIBUTTON|WS_GROUP,10,20,62,10
CONTROL "毁灭恒星",IDC_DESTROY_STAR,"Button"
BS_AUTORADIBUTTON,10,35,55,10

// GROUPBOX 包含两个单选按钮。
// 这种允许单选按钮组合在一起。
CheckRadioButton( hDlg,
                IDC_DESTROY_PLANET,
                IDC_DESTROY_STAR );

// SendDlgItemMessage() 将消息发送给指定的控件。
// 在此例中它是列表框控件，LB_INSERTSTRING 消息用于加载列表中的字符串。
// 应用程序发送 LB_SETCUR 消息来选择字符串并在必要时将其滚动到视图。
// 当选择新字符串时，列表框会移除之前选中字符串的高亮。
for (x=0;PlanetList[x] != NULL;x++)
    SendDlgItemMessage(hDlg,
                   IDC_TARGET_LIST,
                   LB_INSERTSTRING,
                   x,(LPARAM)PlanetList[x] );

SendDlgItemMessage(hDlg, IDC_TARGET_LIST, LB_SETCUR,0,(LPARAM)0 );

// SetDlgText() 设置对话框中控件的标题或文本。
SetDlgItemText(hDlg, IDC_TARGET_VALUE, PlanetList[0]);
SetDlgItemText(hDlg, IDC_MISSION_VALUE, TEXT(" 毁灭行星") );
SetDlgItemText(hDlg, IDC_AUTHORIZATION_CODE, TEXT("ID23"));

break;

// WM_COMMAND 消息在用户从菜单选择命令项、
// 命令向其父窗口发送通知消息，或者快捷键被翻译时发送。
// 在此例中

case WM_COMMAND:
switch ( wParam ) {

// 用户每次点击 IDC_DESTROY_PLANET 单选按钮时都会接收此消息。
case IDC_DESTROY_PLANET :
currentTarget = 0;
SendDlgItemMessage(hDlg,
	IDC_TARGET_LIST,
	LB_RESETCONTENT,
	(WPARAM)0,
	(LPARAM)0);

for (x=0;PlanetList[x] != NULL;x++ )
hDlg,
SendDlgItemMessage(hDlg,
	IDC_TARGET_LIST,
	LB_INSERTSTRING,
	x,
	(LPARAM)PlanetList[x] );

SetDlgItemText(hDlg, IDC_MISSION_VALUE, TEXT(" 毁灭行星"));
SetDlgItemText(hDlg, IDC_TARGET_VALUE, PlanetList[currentTarget]);
SendDlgItemMessage(hDlg,
	IDC_TARGET_LIST,
	LB_SETCURSEL,
	currentTarget,(LPARAM)0 );

break;

// 用户每次点击 IDC_DESTROY_STAR 单选按钮时都会接收此消息。
case IDC_DESTROY_STAR :
currentTarget = 0;
SendDlgItemMessage(hDlg,
	IDC_TARGET_LIST,
	LB_RESETCONTENT,
	(WPARAM)0,
	(LPARAM)0);

for (x=0;StarList[x] != NULL;x++ )
hDlg,
SendDlgItemMessage(hDlg,
	IDC_TARGET_LIST,
	LB_INSERTSTRING,
	x,
	(LPARAM)StarList[x] );

SetDlgItemText( hDlg, IDC_MISSION_VALUE, TEXT(" 毁灭恒星") );
SetDlgItemText( hDlg, IDC_TARGET_VALUE, StarList[currentTarget] );
SendDlgItemMessage( hDlg,
    IDC_TARGET_LIST,
    LB_SETCURSOR,
    currentTarget,
    (LPARAM)0 );

break;

// 确保选择了一个目标。
// 如果用户点击列表框中的任何位置，将发送此消息。
case IDC_TARGET_LIST :

// 发送 LB_GETCURSEL 消息以获取单选列表框中选中项的索引（如果有）。
currentTarget = SendDlgItemMessage(hDlg,
    IDC_TARGET_LIST,
    LB_GETCURSEL,
    0,
    0 );

if (
    SendDlgItemMessage( hDlg,
    IDC_DESTROY_PLANET,
    BM_GETCHECK, 0, 0 ) == BST_CHECKED ) {
    SetDlgItemText(hDlg, IDC_TARGET_VALUE, PlanetList[currentTarget] );
} else {
    SetDlgItemText(hDlg, IDC_TARGET_VALUE, StarList[currentTarget] );
}
break;

// 用户点击 IDC_ATTACK 按钮时接收此消息。
case IDC_ATTACK :
    TCHAR  authorizationCode[255];
    TCHAR  missionString[255];
    TCHAR  targetString[255];
}
}
```

# 570 UNIX 迁移指南

TCHAR executionString[255];

```cpp
// 在单选列表框框中，
// 返回值是基于 0 的当前被 
// 选中项的索引。
// 如果没有选择，返回值为 LB_ERR。
//
currentTarget = =
```

```cpp
SendDlgMessage(hDlg, IDC_TARGET_LIST, LB_GETCURSEL, 0, 0);
//
// GetDlgItemText 函数检索与对话框中的
// 控件关联的标题或文本。
//
GetDlgItemText(hDlg,
    IDC_AUTHORIZATION_CODE,
    authorizationCode,
    32);
GetDlgItemText(hDlg, IDC_MISSION_VALUE, missionString, 32);
GetDlgItemText(hDlg, IDC_TARGET_VALUE, targetString, 32);
```

```cpp
// sprintf 格式函数在缓冲区中存储一系列字符
// 和值。任何参数都会根据格式字符串中相应的
// 格式规范进行转换并复制到输出缓冲区。
//
// 该函数会在其写入的字符末尾附加一个终止
// 空字符，但返回的计数中不包含
// 终止空字符。
//
// 请在基于 Win32 的应用程序中使用此函数而非 sprintf()
//
sprintf(executionString,
TEXT("%s) Authorization Code - %s, Has been carried out!",
missionString,
targetString,
authorizationCode);
// MessageBox 函数创建、显示并操作一个
// 消息框，其中包含应用程序定义的
// 消息和标题，以及任何预定义图标
// 和推送按钮的组合。
//
// MessageBox() 根据第 4 个参数中指定的
// 类型和用户响应返回值。
//
// 它的用法类似于 XMotif 的 XmCreateQuestionDialog
//
dialog = XmCreateQuestionDialog(w, "notice", args, n);
```

```cpp
MessageBox( hDLg,
    executionString,
    TEXT("Mission Execution"),
    MB_OK);
}
break;

case IDC_EXIT:
    DestroyWindow( hDLg );
    break;

default:
    return FALSE;
}
break;

case WM_DESTROY:
    PostQuitMessage( 0 );
    break;

case WM_CLOSE:
{
    DestroyWindow( hDLg );
    break;
///
default:
    return FALSE;
}
return FALSE;

```

+// 此示例应用程序基于 DialogBox。

// WinMain 调用 CreateDialog() 显示该窗口并

// 进入消息循环。

// 这种实现方式可以快速开发

// 需要较小 GUI 的应用程序。

// 然而，没有任何东西阻止大型应用程序

// 使用这种模型。

```cpp
int WINAPI WinMain ( HINSTANCE hInstance, HINSTANCE hPrevInstance, LPSTR
lpCmdLine, int nCmdShow )
{
    MSG msg;
    hInst = hInstance;


+//
// 创建无模态对话框。
```

# 572 UNIX 迁移指南

```cpp
// CreateDialog 宏从对话框模板资源
// 创建一个无模态对话框。
// 该资源存在于 Dialogwindow.rc 中。
hExampleDlg = hInstance,
              CreateDialog(hInstance,
                MAKEMAINTRESOURCE(EXAMPLE_DIALOG),
                (HWND)NULL,
                (DLPROC)ExampleDlgDlgProc );

if ( hExampleDlg != NULL ) {
  ShowWindow(hExampleDlg, SW_SHOW);
}

while ( GetMessage(&msg, NULL, 0, 0 ) ) {
  if ( hExampleDlg == 0 || !IsDialogMessage( hExampleDlg, &msg)) {
    TranslateMessage(&msg);
  }
  DispatchMessage(&msg);
}

return ( msg.wParam );
```

## 迁移测试

本章介绍了对于从 UNIX 迁移到 Microsoft® Windows® 操作系统或 Microsoft Interix 的应用程序建议测试策略。测试是确定迁移后应用程序的预期结果与观察结果之间差异的过程——特别是父应用程序的输出与迁移后应用程序输出之间的对比。只有在按照测试计划对测试结果进行彻底测试和测量后，你才能确定迁移后的应用程序是否满足了所有设计目标。

本章描述了测试目标和建议的发布标准。它还介绍了你可以用于测试应用程序的通用测试流程和方法论。

本章末尾描述的附录提供了测试中使用的各种模板和示例。为了确保对迁移后的应用程序应用适当的测试覆盖，测试这些模板和示例涵盖了以下领域：

- 基础设施
- 安全
- 管理
- 性能

# 迁移项目测试生命周期概述

迁移项目的生命周期与项目的开发阶段同步。在软件生命周期中，测试生命周期遵循瀑布模型、螺旋模型或两者的结合。

# 测试生命周期阶段

在迁移项目中，测试生命周期由以下阶段组成：

- 阶段 1：计划迁移测试。此阶段本质是整个迁移项目计划的一部分，在第4章“评估与分析”中有详细介绍。在此阶段，你建立了主要目标、测试范围、测试标准、进度、基础设施、资源、成功标准以及完成交付物的要求。
- 阶段 2：定义实验室策略并构建测试床。在此阶段，你定义了规划实验室环境、网络配置以及硬件和软件要求的策略。你还创建了测试床。
- 阶段 3：设计测试计划。在此阶段，你根据实验室环境、网络配置以及硬件和软件要求的策略，制定并制定了主要目标、测试范围、测试标准、进度、基础设施、资源、成功标准以及完成交付物的要求。
- 阶段 4：执行测试。在此阶段，你执行测试结果。
- 阶段 5：评估测试。在此阶段，你根据测试结果进行评估。

| 阶段 | 描述 |
| --- | --- |
| 阶段 1 | 计划 |
| 阶段 2 | 定义实验室策略并构建测试床 |
| 阶段 3 | 设计测试计划 |
| 阶段 4 | 执行测试 |
| 阶段 5 | 评估测试 |

（注：原文在阶段描述部分存在多处逻辑重复，此处根据语意进行了翻译对齐）

*纠正：原文描述为：*

红 阶段 1：计划迁移测试...

- 阶段 2：定义实验室策略...
- 阶段 3：设计测试计划计划...
- 阶段 4：执行测试...
- 阶段 5：评估测试...

# 迁移的测试结果

图 12.1 展示了迁移的各个阶段流程。每个阶段的详细信息将在本章后续介绍。

![生命周期概述](img/a2df7b0b951660ea7fa8264598_0)

# 最佳实践

为了确保项目测试阶段成功，建议采取以下最佳实践：

字体 创建主测试计划（MTP）来定义迁移范围。通过维护 MTP，你可以从项目开始跟踪范围。创建一个详细测试计划（DTP）以捕捉所有与测试相关的场景。对于测试用例（DTCs），你可以根据功能、模块或组创建多个文档。为场景创建命名规则（例如 1, 2, 3...），为用例创建命名规则（例如 1.1, 1.2... 2.1, 2.3...）。这非常重要并有助于识别用例。与开发团队评审 DTP，可以提供重要的输入并确保用例的优先级。维护测试计划矩阵，将功能映射到用例 1.2、3.2、1.4、4.5 等。这确保了当需要特定测试时，测试工程师可以添加或修改矩阵。此外，如果功能发生了任何更改或修改或修复修复，可以使用矩阵进行策略性测试。测试计划矩阵的另一个用途是跟踪需求变更并识别测试映射。如果迁移应用程序添加了任何新功能，测试范围；该功能将影响整体测试；你可以使用矩阵有效地跟踪范围。在迁移项目的早期对所有缺陷进行根因分析。测试团队可以根据原因对缺陷进行分类（例如内容、代码、UI、设计或需求错误）。向开发团队提供这些反馈可以确保未来的模块不再包含这些缺陷。通过收集测试指标来确定项目和团队成员的质量和生产力。跟踪每日状态。

# 阶段 1：迁移计划

根据项目的规模和范围，测试经理可以确定适用的测试类型以及如何进行测试。此阶段的输出结果是 MTP，它包含了测试目标、成功标准、项目范围以及本节讨论的其他项目。

MTP 是整个测试生命周期中的一个活动文档。该文档的内容由功能规范和发布计划生成，适用于迁移项目的其他控制程序。附录 12.3，“测试计划模板”是一个包含了迁移所需区域描述的 MTP 示例。

## 测试目标与成功标准

MTP 定义了一系列测试目标，这些目标对于确保项目按计划进行至关重要。迁移测试的类型取决于项目的目标。

定义测试目标和成功标准基本上取决于所考虑的应用：

- **功能。** 迁移后的应用程序在 Windows 平台上应具有与 UNIX 平台相同的功能。例如，如果迁移后的应用程序必须支持 200 个客户端（与 UNIX 应用程序相比），这是测试计划范围。
- **互操作性。** 该部分的参数是应用程序是否需要交换数据。确保互操作性可以减少数据转换的复杂性。关于互操作性的更多信息，请参阅第 5 章，“迁移计划”。
- **性能。** 相比于 UNIX 系统（例如 Sun Sparc 或 HP-UX），Windows 平台上的整体性能是否可以接受取决于迁移项目的目标。如果目标是在 Windows 平台上获得更高的性能，测试阶段必须彻底涵盖性能。你可以尽可能通过基准测试来衡量性能，或者根据开发人员的分析来衡量性能。

根据前面的测试参数，可以在表 12.1 中定义成功标准：

# 表 12.1 测试通过与失败标准

| 成功标准 | 通过定义 | 失败定义 |
| --- | --- | --- |
| 功能 | 迁移后的应用程序在 Windows 环境中具有与 UNIX 平台相同的功能。 | 迁移后的应用程序未能提供相同的功能。 |
| 互操作性 | 迁移后的应用程序可以在无转换的情况下，访问现有的数据或项目文件。 | 迁移后的应用程序无法访问现有数据或项目文件，且转换过程非常复杂。 |
| 性能 | 迁移应用程序符合在项目范围内定义的性能目标。 | 迁移应用程序未达到性能目标。 |
