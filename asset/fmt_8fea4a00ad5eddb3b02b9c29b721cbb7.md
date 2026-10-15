
```
reg save HKLM\sam sam
reg save HKLM\system system
```

让我们看看 OSSEM 关于这种技术告诉了我们什么。

## 实验 9-1：使用 OSSEM 可视化数据源

访问 `https://ossemproject.com/dm/mitre_attack/attack_technique_to_events.html`。

然后，将鼠标悬停在网站右上角的火箭（发射）图标上，点击 Binder 在 Binder 网站上免费启动 Jupyter notebook。

## 从 ATT&CK 技术到安全事件

- 作者：Jose Luis Rodriguez -@Cyb3PandaH
- 组织：Open Threat Research (OTR)
- 参考文献：

此 Jupyter notebook 允许通过浏览器的便利性和安全性，对 Python 及其所有相关库进行实时、交互式的处理。加载需要一些时间（毕竟它是免费的，感谢网站页面顶部列出人员的慷慨捐赠）。加载完成后，你将看到以下屏幕。点击灰色代码块，然后点击顶部的 Run (运行) 按钮或按 SHIFT-ENTER 来处理该代码块。

![](img/0add480ffb73b6bc89b65d99f7d6b37a_328_0.png)

继续执行下一块代码。运行将需要一段时间，因为正在拉取并解析 MITRE ATT&CK 技术。在运行期间，你会注意到代码块左侧有一个括号中的星号 ([*])。完成后，星号将变为代表该代码块的数字。`head()` 命令将显示映射中的前五个项，从 0 开始，如下所示：

```python
In [2]: yamluri = 'https://github.usercontent.com/mitre/attack/OSSEM-DM/master/main/use-cases/mitre_attack/techniques_to_events_mapping.yaml'

yamlContent = requests.get(yamluri).text

yaml = yaml.safe_load(yamlContent)

mapping = yaml.json_normaliser(nyaml)

print(mapping):
```

```python
Out[2]:
| technique_id | mitre_technique | tactic | platform | data_source | data_component | name | relationship | target |
|---|---|---|---|---|---|---|---|---|
| 0 | T1053.002 | Process Modification | (defense-evasion) | windows | windows registry key | Windows process | modified registry | windows key |
| 1 | T1053.002 | Code Signing | (defense-evasion) | windows | windows registry key | Windows process | modified registry | key |
```

稍等片刻，你可以继续执行后续代码块（每块代码由其之前的标题和文本进行解释），这些代码使用 OSSEM 显示 T1003.002 子技术的数据源和组件。调整代码以测试 T1003.002，如下所示。这就是 Jupyter notebook 的魅力之处：它们是动态的，你可以对它们进行实验来学习。

### 推荐的数据源有哪些？

```python
In [7]: mapping['technique_id'][['data_source']]
Out[7]:
| data_source | data_component |
|---|---|
| 4285 | command execution |
| 4293 | windows registry key |
| 4297 | registry key |
```

在这里，我们可以看到 `command execution`、`windows registry key` 和 `registry key` 分别是 T1003.002 的数据源。

```python
In [8]: mapping['technique_id'][['data_component']]
Out[8]:
| data_component | name |
|---|---|
| 4285 | windows registry key |
| 4293 | windows registry key |
| 4297 | registry key |
```

```python
In [9]: mapping['technique_id'][['name']]
Out[9]:
| name | relationship |
|---|---|
| Windows process | modified registry |
| Windows process | modified registry |
| Windows process | modified registry |
```

等等，映射显示：

| technique_id | mitre_technique | tactic | platform | data_source | data_component | name | relationship | target |
|---|---|---|---|---|---|---|---|---|
| 0 | T1053.002 | Process Modification | (defense-evasion) | windows | windows registry key | Windows process | modified registry | windows key |
| 1 | T1053.002 | Code Signing | (defense-evasion) | windows | windows registry key | Windows process | modified registry | key |

现在，让我们看看 T1003.002 的视化结果。

```python
In [10]: vis.graph(mapping[mapping['technique_id']=='T1003.002'])
```
