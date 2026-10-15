
`\`使`C-w`被解释为`CONTROL-W`而不是三个字母（等同于`\W`）。命令名称前的未匹配单引号是正确的。这是一个 Lisp 转义字符，用于防止名称被过早求值。

## 示例 .emacs 文件

以下`.emacs`文件产生了一个纯编辑环境，为我们用户减少了干扰。当然，如果任何部分或行不适用或不符合你的喜好，你可以编辑它或使用一个或多个`;`注释字符将其注释（位于第一列）。

### 偏好变量

```lisp
(set make-backup-files nil)

(set backup-by-copying t)

(set delete-auto-save-files t)

(set blink-matching-parent nil)

(set default-case-search nil)

(set require-newline ask)
```

```lisp
;; 不备份文件

;; 如果要备份，至少不要破坏链接

;; 在写入 org 时删除自动保存的文件

;; 不要让匹配的父括号闪烁

;; 搜索时不区分大小写

;; 缺少末尾换行符时询问
```

```lisp
;; 为 C-h 和 DEL 设置反向映射
(keyboard-translate \?C-h \?177)
(keyboard-translate \?177 \?C-h)
```

```lisp
;; C-w 原本应该是 kill-region，但对受过 vi 训练的手指来说是很大的负担。
;; 改为绑定 backward-kill-word 以获得更熟悉、友好的行为。
(define-key global-map "\^W" 'backward-kill-word)
```

```lisp
;; 对于 kill-region 使用双键序列 c-x c-k。
(define-key ctl-x-map "\^k" 'kill-region)
```

## 第 11 章 emacs 编辑器

```lisp
(require 'cc-mode')
;kiss: 确保它在这里
```

```lisp
(c-add-style
bsd8
;添加缩进样式
old bsd (8 个空格)
'((c-basic-offset 8)
(c-hanging-comment-ender-p . nil) ; 隔离的 "*" 结束块注释
(c-comment-only-line-offset 0)
(c-offsets-list . ((statement-block-intro +))
(knr-argdecl-intro +)
(substatement-open 0)
(label 0)
(statement-cont . +))))
```

```lisp
)
(add-hook
'c-mode-hook
(function
(lambda ()
(c-set-style "bsd8")))
;这是我们的默认样式，
;始终在 c-mode-hook 中设置它。)
```

```lisp
;; c mode 样式设置结束
```
