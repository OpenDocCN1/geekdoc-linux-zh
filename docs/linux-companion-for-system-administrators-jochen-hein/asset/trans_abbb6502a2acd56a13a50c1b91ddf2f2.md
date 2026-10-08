
通过这些关键字，你将找到一个（特定于缓冲的）变量名，后面是一个冒号和该变量的新值。这可以用于为给定的文件定义特殊的缩进样式，例如。

```
% Local variables:
% mode: latex.
% Tex-master: "master"
% End:
```

Listing 5.6 LaTeX 源代码中局部变量的示例。

Listing 5.6 显示了 LaTeX 源代码中局部变量的示例。
这些变量由 `auctex` 模式评估，遗憾的是，该模式并不是 GNU Emacs 标准发行的一部分；XEmacs 包含了这个包。
该模式可以用于 Tex 和 LaTeX 文件，`mode` 变量始终用于选择模式。上面的文件是构成文档的多个文件之一；由 LaTeX 处理的主行被称为 `master`。

如果变量 `enable-local-variables` 为 `t`，则会考虑局部变量；如果值为 `nil`，则会忽略这些变量。任何其他值都会显示相应的代码块，并询问用户是否设置这些变量。

这种机制还允许在 Emacs 中实现宏，因为许多 Emacs 函数都受到变量的影响，归根结底它们只是具有特殊内容的变量。因此，不应盲目接受来自外部文档的局部变量，而应该检查它们，并在必要时拒绝请求。`ignored-local-variables` 变量也可以用于排除特定变量的修改。例如，Listing 5.7 包含了 XEmacs 的默认设置。此设置可以防止在第一个文件上发出初始提示，然后在后续所有文件中都处于禁用状态。列表中可能还包含额外的变量。

```
;; The following variables cannot be buffer-specific.
(setq ignored-local-variables '(enable-local))
```

Listing 5.7 变量 `ignored-local-variables`。

## 5.3.4 作为服务器的 Emacs – 多人共用

各种程序（例如 `em` 和 `cron`）可以调用任意编辑器来编辑文本。通常，这些程序使用环境变量 `EDITOR` 或 `VISUAL`，其中包含编辑器的名称。如果这些变量仅包含 `emacs`，则每次调用时都会启动一个新的 Emacs 进程。这在实践上是不可行的，因为会消耗时间和内存；此外，Emacs 进程无法访问彼此的缓冲区（buffers）。因此，真正的 Emacs 用户会在 Emacs 内部启动一切，这些进程会持续到注销。

通过将 Emacs 配置为服务器，可以使用运行中的 Emacs 作为新缓冲区的编辑器（例如从 `em` 调用）。为此，必须在 Emacs 内部调用函数 `server-start`。这可以通过在 `~/.emacs` 文件中的适当条目来实现自动化。其结果是，每当应用程序调用 `emacsclient` 时，就会向 Emacs 服务器发送一条消息，要求其将特定文件加载到新缓冲区中。如果是虚拟控制台，你必须切换到控制台 Emacs；当你完成服务器中文本的编辑后，通过 `C-x` 离开缓冲区，之前编辑的缓冲区将再次显示在窗口中。然后会向 `emacsclient` 发送消息，要求其终止。因此，这些程序与直接调用编辑器没有区别。整个过程在文本控制台上同样适用。在这里，在一个控制台上启动 Emacs 并在另一个控制台上使用它比反复启动更实用，因为切换控制台比完全加载 Emacs 要快。虽然配置需要很长时间，但这种做法是值得的。

## 5.3.5 作为服务器的 Emacs – 更多功能

GNU Emacs 作为服务器提供的函数并不总是够用的。因此，无法让运行中的进程评估单个 Lisp 表达式。为了避免 GNU Emacs 和 XEmacs 之间的冲突，XEmacs 使用了不同的 Lisp 函数，你应该编写你的 Lisp 文件，使其能够同时在两个编辑器上使用。如果没有安装 Emacs，或者你经常在两个环境之间切换，这将非常有用。

在 Emacs 中，通过函数 `server-start` 启动服务器。Listing 5.8 显示了如何在 Lisp 函数内部区分 GNU Emacs 和 XEmacs 的示例。

```
; 运行的是哪个？XEmacs 还是 GNU Emacs?
(defvar running-emacs
  (string-match "XEmacs\|GNU Emacs" version))
(cond
  (not running-emacs)
    (setq GNU Emacs-specific-code
      (server-start))
  (t; Emacs-specific-code
    (server-start))))
```

**Listing 5.8** 为 GNU 和 XEmacs 自动启动 Emacs 服务器。

随后，你可以完全像使用 `emacs` 一样使用 `emacsclient` 程序。唯一的区别是缓冲区的处理也可以从另一台计算机进行。为此，必须执行基于主机的认证或密码检查。如果 Emacs 安装正确，可以使用 `xauth` 程序；它会使用显示器编号。

GNU Emacs 特别有意思的扩展是 `scratch` 和 `remote` 程序。通过 `scratch`，可以说服一个已经在运行的 Emacs 在当前终端上接受额外输入。当人们通过调制解调器登录或坐在同事的工作站前，且无法或不希望启动新的 Emacs 时，这非常有用。然而，键盘映射和颜色可能与当前终端不匹配，因为这些通常只在 Emacs 启动时执行一次。

`remote` 程序用于让 Emacs 评估 Lisp 表达式。调用示例可以在 `remote` 的手册页中找到。通过这种方法的安全影响与 `scratch` 相同。

## 5.4 键盘映射

除了通过菜单（在 X 下）调用、快捷键以及 `M-x` 命令调用，几乎所有的键都可以关联到函数。Emacs 区分适用于所有模式的全局映射和针对特定模式的局部映射。

请注意，许多模式在局部表中重新定义了按键，因此映射会在缓冲区之间发生变化。Listing 5.9 显示了全局和局部键盘表的示例。请注意，许多键的表示在 GNU Emacs 和 XEmacs 之间不同；这在短期内可能改变。

```
; 全局适配
(global-set-key [home] 'beginning-of-line)
(global-set-key [end] 'end-of-line)
(global-set-key "C-g" 'goto-line)
```

```
; LaTeX 键盘映射适配
(defun my-latex-mode-hook ()
  (define-key Latex-mode-map '[delete] 'delete-character))
(add-hook 'latex-mode-hook' 'my-latex-mode-hook')
```

Listing 5.9 键盘映射的适配。
