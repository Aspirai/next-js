### VSCode常用命令

#### 1.强制折叠代码块

```
//#region
...
//#endregion
```

#### 2.自动保存设置

首选项----设置----搜索Auto Save----afterDelay----Auto Save Delay----100

#### 3.代码片段设置

文件----首选项----用户片段
body中的'$1'代表输入后光标停留位置；

#### 4.自动折叠代码块

```
操作光标所在文件中的所有代码块：
    折叠所有 Ctrl+K+0
    展开所有 Ctrl+K+J
仅仅操作光标所处代码块内的代码：
    折叠 Ctrl+Shift+[
    展开 Ctrl+Shift+]
可以使用Ctrl+Shift+P搜索fold和unfold，以查看更多选项。
```

```
1.打开快捷面板
Ctrl + K + S

2.打开键盘帮助面板
Ctrl + K + R
```

## VS Code用户指南与使用技巧

  📅 2020.02.28      ·  ☕ 20 分钟           

- [#vscode](https://www.thisfaner.com/t/vscode/)

## 一、User Guide（用户指南）

> 参考官方文档：[Basic Editing in Visual Studio Code](https://code.visualstudio.com/docs/editor/codebasics)

## 更改显示语言

通过安装插件 `Chinese (Simplified) Language Pack for Visual Studio Code` 来启用中文（需要重启）

默认情况下，Visual Studio Code 附带英语作为显示语言，而其他语言则依赖于 Marketplace 提供的语言包扩展。

VS Code 检测到操作系统的 UI 语言，并会提示您安装适当的语言包（如果在 Marketplace 上可用）。

## 保存/自动保存

默认情况下，VS 代码需要一个明确的行动，将更改保存到磁盘，按`Ctrl + S`。

您也可以使用**文件** > **自动保存**从顶级菜单切换**自动保存**。

要进一步控制自动保存，请打开配置文件`settings.json`，然后找到相关的设置（如果没有则直接添加）：



```
"files.autoSave": "off" 
```

它可以具有以下值：

- `off` -禁用自动保存。
- `afterDelay` - 在配置的延迟（默认 1000 毫秒）后保存文件。
- `onFocusChange` - 当焦点移出脏文件的编辑器时保存文件。
- `onWindowChange` - 当焦点移出 VS Code 窗口时保存文件。
- `files.autoSaveDelay`：当`files.autoSave`配置为时，配置延迟（以毫秒为单位）`afterDelay`。默认值为 1000 毫秒。

> 打开用户设置 `settings.json` 文件的方法，你可以通过在命令面板（打开命令面板的快捷键为 F1 ）输入命令：`Open Settings (JSON)` 来打开此文件。

## 预览模式

在 VS Code 中打开工作区内的文件的方式：

- 单击文件，进入预览模式，此时标签页中的名字显示为 *斜体*
- 双击文件，直接进入编辑模式，此时标签页中的名字正常显示

在资源管理器中单击或选择一个文件时，该文件将以 **预览模式** 显示并重用现有选项卡。 如果您正在快速浏览文件，并且不希望每个访问的文件都有其自己的标签页，则这非常有用。 当您开始编辑文件或使用双击从资源管理器中打开文件时，会有一个新的标签页专用于该文件。

预览模式在标签页标题中以 ***斜体*** 表示

![img](https://code.visualstudio.com/assets/docs/getstarted/userinterface/preview-tab.png)

如果在预览标签页中编辑文件，或者双击该预览标签页，则该标签页自动变为编辑模式。

如果您不想使用预览模式而希望总是创建一个新的标签页，则可以使用以下设置来控制：

- `workbench.editor.enablePreview` ：全局启用或禁用（`false`）预览编辑器
- `workbench.editor.enablePreviewFromQuickOpen` ：启用或禁用预览编辑器，当从“快速打开（Ctrl + P）” 中打开文件时。

## 代码补全

### 手动代码补全

手动代码补全：默认 快捷键为 `Ctrl + 空格键` ，但是在 Windows 中它被系统输 入法非法占用（当按下此快捷键时出现中英切换提示，它被用于中/英模式切换）；解决方法：

- 方法一：修改 vscode 中的快捷键，比如 `Alt+/`；或者在 `keybindings.json` 中为触发建议 **再添加一个快捷键** 。
- 方法二：设置自动补全（无需按快捷键）
- 方法三：等待微软的补丁包（几十年了都没见到）
- 方法四：抛弃Windows系统。

### 自动代码补全

全局配置：用于所有语言，在 `settings.json` 文件中添加



```
  // 在编辑时是否自动提示补全  "editor.quickSuggestions": {    "other": true,    "comments": true,    "strings": true  }, 
```

**用于特定语言：**

比如为 markdown 文件开启 **自动补全**，在 `settings.json` 文件中添加如下配置：



```
  "[markdown]": {    // 快速补全    "editor.quickSuggestions": {      "other": true,      "comments": true,      "strings": true    },    // 显示空格    "editor.renderWhitespace": "all",    // snippet 提示优先（看个人喜欢）    "editor.snippetSuggestions": "top",    "editor.tabCompletion": "on",    // 使用enter 接受提示    // "editor.acceptSuggestionOnEnter": "on",  }, 
```

开启之后，可以自动提示  markdown 的 snippet；比如：

- 输入 `code` 就会弹出行内代码和代码块两种补全提示
- 输入 `ul` 或 `li` 就会弹出列表补全提示
- 类似的还有 `bold` 、`image`、`italic`、`link` 、`quote` 等。

## 格式化

VS Code 对源代码格式有很好的支持：

- **格式化文档**（Shift + Alt + F）- 格式化整个活动文件。
- **格式选择**（Ctrl + K Ctrl + F）- 格式化所选文本。

如果您自行安装了格式化扩展程序，并可以提供相同语言的格式设置，可以选择禁用默认语言格式程序：



```
"html.format.enable": false 
```

除了手动调用代码格式外，您还可以根据用户手势（例如键入，保存或粘贴）来触发格式化。默认情况它们是关闭状态，但是您可以通过以下设置启用这些行为：

- `editor.formatOnType` - 输入后进行 行格式。
- `editor.formatOnSave` - 保存时格式化文件。
- `editor.formatOnPaste` - 格式化粘贴的内容。

> 注意：并非所有格式化程序都支持粘贴时格式化，前提是它们必须支持格式化所选内容或文本范围。

## 缩进

默认情况下，VS Code 将每个 Tab 键替换为 4 个空格。如果您想更改默认设置，则可以修改`editor.insertSpaces`和`editor.tabSize`



```
//是否替换 "editor.insertSpaces": true, "editor.tabSize": 4, 
```

**自动侦测：**

VS Code 会分析打开的文件并确定文档中使用的缩进。自动检测到的缩进将覆盖您的默认缩进设置。检测到的设置显示在状态栏的右侧：

![indentation-detection.png](https://i.loli.net/2020/02/28/Qg8GPkuxvlOET3t.png)

可以单击"状态栏"缩进 显示（上图中的`Tab Size:4`），来更改缩进方式。

## 查找和替换

VS Code 允许您快速查找文本并替换为当前打开的文件。按`Ctrl + F`在编辑器中打开 “查找小部件” （Find Widget），搜索结果将在编辑器，概述标尺和小地图中突出显示。

如果当前打开的文件中有多个匹配结果，则可以在查找输入框处于焦点状态时按`Enter`和`Shift + Enter`导航到下一个或上一个结果。

“查找小部件” （Find Widget）还可以调整大小：

![resize-find-widget.gif](https://i.loli.net/2020/02/28/ZzaRxPSsDLmkUE6.gif)

**在选中的文本中查找 ：**

默认情况下，查找操作在编辑器中的整个文件上运行。它也可以在选定的文本上运行。您可以通过单击"查找"小部件上的 三明治图标 来启用此功能。

![find-in-selection.gif](https://i.loli.net/2020/02/28/PKhvVwMjzJbZxu3.gif)

**搜索多行文本：**

您可以通过将文本粘贴到"查找"输入框和"替换"输入框中来搜索多行文本。按下`Ctrl+Enter`将在输入框中插入新行。

![multiple-line-support.gif](https://i.loli.net/2020/02/28/GcbkpHzEnyjwmiJ.gif)

**搜索文件：**

按`Ctrl + Shift + F`并输入搜索词

## 常见问题

**是否可以进行全局搜索和替换？**

可以；展开搜索视图文本框以包含替换文本字段。您可以搜索和替换工作空间中的所有文件。

**如何打开自动换行？**

您可以通过 `editor.wordWrap` 设置控制自动换行

您可以使用`Alt + Z`切换 VS Code 会话的自动换行。

## 二、技巧和窍门

> 官方文档：[Visual Studio 代码提示和技巧](https://code.visualstudio.com/docs/getstarted/tips-and-tricks)

## 命令面板

根据您的当前上下文访问所有可用命令。

按键盘快捷键：`Ctrl + Shift + P` 或 `F1` 弹出的对话框叫"命令面板"

![OpenCommandPalatte.gif](https://i.loli.net/2020/02/28/SGMA6qR9sC5oUei.gif)

- `ctrl + shift + p` 和 `F1`：打开命令面板时会带有 `>`
- `ctrl + p`: 打开命令面板时没有 `>` ，此时它的作用是 快速打开 某个文件

由于快捷键冲突而导致无法触发相应插件，解决方法之一是直接在命令面板中操作。

## 快速开启

快速打开文件。

如果一个文件夹中包含的文件较多，使用命令面板寻找并打开文件是不错的选择。

键盘快捷键：`Ctrl + P`

![QuickOpen.gif](https://i.loli.net/2020/02/28/VnIj18LOEXoMDTC.gif)

在最近打开的文件之间导航： **重复 快速打开 ，以在最近打开的文件之间快速循环** 。

从快速打开中打开多个文件： **按鼠标中键，在后台打开文件** 。

提示：在打开该对话框后输入不同的内容可以进行不同的操作：

```
直接输入文件名，快速打开文件

>   显示并执行命令
?   取帮助
:   跳转到行数，也可以Ctrl+G直接进入(Mac 是 CMD+G)
@   到symbol（搜索变量或者函数），也可以Ctrl+Shift+O直接进入
@   分类跳转symbol，查找属性或函数，也可以Ctrl+Shift+O后输入:进入
#   根据名字查找symbol，也可以Ctrl+T
```



## 状态栏

一、错误和警告：

快捷键：`Ctrl + Shift + M`

作用：快速跳转到项目中的错误和警告。

也可以通过点击状态栏中的按钮来打开：![状态栏警告](https://i.loli.net/2020/02/28/N7b4OpFiMwhGDem.png)

通过  `F8 `或`Shift + F8`循环检查错误

![Errors_Warnings](https://i.loli.net/2020/02/28/7Ign9b2Qx341VXD.gif)

你可以按类型（“错误”，“警告”）或文本匹配来过滤问题。

## 调整设置 ⭐

户设置 `settings.json` 文件，你可以通过（命令面板）输入命令：`Open Settings (JSON)` 来打开此文件。

格式



```
"editor.formatOnPaste": true 
```

更改各种 UI 元素的字体大小



```
// Main editor "editor.fontSize": 18, // Terminal panel "terminal.integrated.fontSize": 14, // Output panel "[Log]": {    "editor.fontSize": 15 } 
```

更改缩放等级



```
"window.zoomLevel": 5 
```

使用连体字



```
"editor.fontFamily": "Fira Code", "editor.fontLigatures": true 
```

> **提示：**您将需要安装支持字体连字的字体。[FiraCode](https://github.com/tonsky/FiraCode)是 VS Code 团队中流行的字体。微软新开发的编程字体 Cascadia Code 也支持。
>
> 连体字效果：
>
> ![font-ligatures-annotated.png](https://i.loli.net/2020/02/28/x5W1r6ZPFEgBnaq.png)

自动保存（另见上文）



```
"files.autoSave": "afterDelay" 
```

您也可以使用 **文件** > **自动保存**从顶级菜单切换**自动保存**。

保存时格式化



```
"editor.formatOnSave": true 
```

更改制表符的大小



```
"editor.tabSize": 4 
```

是否使用空格替换制表符



```
"editor.insertSpaces": true 
```

渲染空白



```
"editor.renderWhitespace": "all" 
```

忽略文件/文件夹

从编辑器窗口中排除这些文件/文件夹。



```
"files.exclude": {    "somefolder/": true,    "somefile": true } 
```

从搜索结果中排除这些文件/文件夹。



```
"search.exclude": {    "someFolder/": true,    "somefile": true } 
```

**专用于特定编程语言的设置：**

对于只需要特定语言的设置，您可以按语言标识符确定设置的范围。您可以在" [语言标识符"](https://code.visualstudio.com/docs/languages/identifiers)参考中找到常用语言 ID 的列表。



```
"[languageid]": { } 
```

> 你可以通过在命令面板中输入命令：`Configure Language Specific Settings` 来进行设置。

## 文件和文件夹 ⭐

使用快捷键 `Ctrl + ` `打开终端

通过 菜单 👉 文件 👉 自动保存 来切换自动保存。

切换边栏：`Ctrl + B`

### 禅模式

禅模式： 进入无干扰的禅模式 `Ctrl + KZ` ；按两次 `Esc` 退出。

![zen_mode.gif](https://i.loli.net/2020/02/28/h8p6dAPS1lo2ZLE.gif)

### 并排编辑

快捷键：`Ctrl + \`

您还可以拖放编辑器以创建新的编辑器组，并在组之间移动编辑器。

![split_editor.gif](https://i.loli.net/2020/02/28/UOnghvD2xC6EurB.gif)

### 在编辑之间切换

键盘快捷键：`Ctrl + 1，Ctrl + 2，Ctrl + 3`

![navigate_editors.gif](https://i.loli.net/2020/02/28/nRrctvLgWECbVYZ.gif)

### 创建或打开文件

键盘快捷键：`Ctrl +单击`

您可以通过将光标移动到文件链接并使用 Ctrl + click 来快速打开文件或图像或创建新文件。

![create_open_file.gif](https://i.loli.net/2020/02/28/hYAIWUDgoExX9w7.gif)

### 导航历史

浏览整个历史记录：`Ctrl + Tab`

向后导航：`Alt +向左`

向前导航：`Alt +向右`

![navigate_history.gif](https://i.loli.net/2020/02/28/ocihrs8P9zqBZ1V.gif)

### 文件关联

为未正确检测到的文件创建语言关联。例如，许多带有自定义文件扩展名的配置文件实际上是 JSON



```
"files.associations": {    ".database": "json" } 
```

## 编辑技巧 ⭐

### 多光标选择

使用 `Ctrl+Alt+Down`或`Ctrl+Alt+Up` 在当前光标的下方或上方再插入一个光标。

![multicursor.gif](https://i.loli.net/2020/02/28/YMCAxivuaNK1pmO.gif)

`Ctrl+D` ： 选中下一个与当前光标下相同的单词 （Add selection to next Find match）

![multicursor-word.gif](https://i.loli.net/2020/02/28/YXNsyCHm2gKS19A.gif)

另外还可使用 `Ctrl + Shift + L` ：Select all occurrences of current selection；选中文件中所有相同的字符串

> 当然这些操作都可以通过 菜单 👉 选择 来进行操作

### 多光标修饰符

多光标修饰符是用来设置我们如果配合鼠标单击来添加多个光标。比如，当我们可以通过 `Ctrl + 单击` 添加多个光标时，`Ctrl` 键就是 `多光标修饰符`

多光标修饰符可以二选一，通过配置 `editor.multiCursorModifier` 来进行设置， 可以设置为：

- `ctrlCmd`- 它在 Windows 上映射为 Ctrl，在 macOS 上映射为 Cmd。
- `alt`- 即 Alt。

可以通过" **选择"**菜单 👉 " **切换为 Ctrl/Alt +单击 进行多光标功能** " 来快速切换此设置。

多光标修饰符的其他影响：

" **转到定义** " 和" **打开链接**" 的手势也将遵守此设置并自动进行调整，以使其不会冲突。例如，

- 当设置为`ctrlCmd`时，可以使用`Ctrl/Cmd + 单击`添加多个光标，而需要使用`Alt + 单击`进行打开链接或转到定义
- 当设置为 `Alt` 时， 可以使用 `Alt + 单击` 添加多个光标，而需要使用`Ctrl/Cmd + 单击`进行打开链接或转到定义

### 缩小/扩大 选择

扩大选中区域： `Shift + Alt + Right`

缩小当前选择：使用 `Shift + Alt + Left`

![expandselection.gif](https://i.loli.net/2020/02/28/ConjAOYI5fxuwPF.gif)

### 列（框）选

通过 `Shift+Alt+鼠标拖动`，

将光标放在一个角上，然后在按住`Shift + Alt`的同时拖动到对角：

在 code >= 1.43 的版本中，也可以通过 菜单 👉 选择 👉 列选模式；来直接进入列选模式，进入列选模式后会在状态栏显示`Column Selection（列选）`，单击此图标可以退出列选模式。

注意：当使用 `Ctrl` 作为多光标修改器时，这将更改为 `Shift + Ctrl`

![column-select.gif](https://i.loli.net/2020/02/28/qx8c9fdkZoDrAFl.gif)

### 移动多个光标

多光标移动，实现方法：多光标插入 配合`Ctrl + 方向键`

多光标插入：可以是上文介绍的任意一种方式。

### 撤消光标位置

键盘快捷键：`Ctrl + U`

在进行多光标插入时如果某个光标位置错误还可以使用 `Ctrl + U` 进行撤销上次插入。

### 选择当前行

键盘快捷键：`Ctrl + L`

> 或者尝试 `Ctrl + i`

### 快速滚动

**快速滚动：** 按 Alt 键可在编辑器和资源管理器中（5 倍）快速滚动。

### 上下复制行

键盘快捷键：`Shift + Alt +向上键`或 `Shift + Alt +向下键`

![copy_line_down.gif](https://i.loli.net/2020/02/28/wWr6lEVFduSOqfk.gif)

### 上下移动行

键盘快捷键：`Alt + Up`或`Alt + Down`

![move_line.gif](https://i.loli.net/2020/02/28/ntb8IQm4T1WCMED.gif)

### 转到文件中的 Symbol

符号查找

键盘快捷键：`Ctrl + Shift + O`

![find_by_symbol.gif](https://i.loli.net/2020/02/28/StlPMAcFi4GNX1y.gif)

您可以通过添加冒号来按种类对符号进行分组`@:`。

![group_symbols_by_kind.png](https://i.loli.net/2020/02/28/2Iwr9KOZpQJavg8.png)

### 转到工作区中的 Symbol

键盘快捷键：`Ctrl + T`

![go_to_symbol_in_workspace.png](https://i.loli.net/2020/02/28/Wl6d1NHqzZ3TajP.png)

### 导航到特定行

键盘快捷键：Ctrl + G

### 修剪尾随空格

键盘快捷键：Ctrl + K Ctrl + X

![trim_whitespace.gif](https://i.loli.net/2020/02/28/a6gb5E19JWZuhFN.gif)

### 括号匹配

- Mac: `cmd+shift+\`
- Windows / Linux: `ctrl+shift+\`

### 代码格式化

当前选择的源代码：Ctrl + K Ctrl + F

整个文档格式：Shift + Alt + F

![img](https://code.visualstudio.com/assets/docs/getstarted/tips-and-tricks/code_formatting.gif)

### 代码折叠

键盘快捷键：`Ctrl + Shift + [`和`Ctrl + Shift +]`

![代码折叠](https://code.visualstudio.com/assets/docs/getstarted/tips-and-tricks/code_folding.gif)

### 导航到文件的开头和结尾

键盘快捷键：`Ctrl + Home`和`Ctrl + End`

### 打开 Markdown 预览

在 Markdown 文件中使用

键盘快捷键：`Ctrl + Shift + V`

并排 Markdown 编辑和预览：`Ctrl + KV`

## 智能感知

我们将始终提供单词补全功能。我们也提供了真正的 IntelliSense 体验。如果语言服务知道可能的补全，则在您键入时会弹出 IntelliSense 建议。

`Ctrl + Space`触发"建议"小部件。

![intellisense.gif](https://i.loli.net/2020/02/28/dnUGWqYa4K5bfJN.gif)

默认情况下，`Tab` 或 `Enter` 表示接受当前选项

您可以查看可用的方法，参数提示，简短文档等。

### 查看定义（peek 视图）

选择一个符号，然后按`Alt + F12`。或者，使用上下文菜单，选择 快速查看 👉 查看定义。

![peek.gif](https://i.loli.net/2020/02/28/hxESniZj8ACo9VL.gif)

### 转到定义

选择一个符号，然后按 F12 或 `Ctrl + 单击`，或者使用上下文菜单。

![转到定义](https://code.visualstudio.com/assets/docs/getstarted/tips-and-tricks/goto_definition.gif)

您可以使用`Go > Back`命令或`Alt + Left`返回到先前的位置。

### 查看引用

选择一个符号，然后按`Shift + F12`。或者，使用上下文菜单 👉 快速查看 👉 查看引用。

![find_all_references.gif](https://res.cloudinary.com/faner/image/upload/v1584603422/hugo/tools/vscode/find_all_references_axyoud.gif)

```
![原图失效：find_all_references.gif](https://i.loli.net/2020/02/28/Rio5G8FBuJkVqPh.gif)
![备用find_a_r.gif](https://i.loli.net/2020/03/19/3XsHlykCFwJZYo9.gif)
```



### 查找所有引用

查找所有文件中的引用，Find All References view

选择一个符号，然后按`Shift + Alt + F12`打开 “引用"视图，在侧边栏中显示文件的所有符号。

### 重命名符号

重构重命名：选择一个符号，然后按 F2 。或者，使用上下文菜单（右键菜单）👉 重命名。

![rename_symbol.gif](https://i.loli.net/2020/02/28/Sy1jN3sWhx6moav.gif)

### Emmet 语法

[支持 Emmet 语法](https://code.visualstudio.com/docs/editor/emmet)。

![Emmet语法](https://code.visualstudio.com/assets/docs/getstarted/tips-and-tricks/emmet_syntax.gif)

## Snippets（代码片段）

> [Snippets in Visual Studio Code](https://code.visualstudio.com/docs/editor/userdefinedsnippets)

**触发提示** 时（`Ctrl + Space`） ：会显示 Snippet（代码片段） 。

可以从 Marketplace 安装扩展从而来提供 snippets。

- vscode-sinppet ：适用于多种语言。才知道还有这么个**作弊网站** [cheat.sh](https://cht.sh/)
- snippet-creator ：简化 snippet 的创建。 Select the code you want to create snippet from and use command `Create Snippet` from the command palette

### 创建自定义 Snippets

文件 👉 首选项 👉 用户代码片段 👉 选择该 snippet 用于哪种类型的文件或选择 Global Snippets 文件



```
"create component": {    "prefix": "component",    "body": [        "class $1 extends React.Component {",        "",        "\trender() {",        "\t\treturn ($2);",        "\t}",        "",        "}"    ] }, 
```

在[创建自己的代码段中](https://code.visualstudio.com/docs/editor/userdefinedsnippets)查看更多详细信息。

## Git 集成

键盘快捷键：`Ctrl + Shift + G`

Git 集成随 VS Code 一起提供。您可以从扩展市场中安装其他的 SCM 提供程序。

克隆远程仓库：

`ctrl + shift + p` 打开命令面板，输入`>Git:clone`回车并且输入仓库地址即可。

查看到当前文件修改状态：

1. 文件名旁边有个`+ M`，代表修改了文件但是没有暂存。可以点击`+` 就可执行`git add` 进行暂存，**点击`M`可以进行差异比较**。
2. 文件名旁边有`- M` 已暂存，但是没有提交
3. 文件名旁边 `U` 表示该文件为新建的文件，还没进行跟踪。

可以从左下角 git 状态栏 查看当前分支是否有未更新的代码等。

### Diffs 差异比较

在 " **源代码管理”** 视图中，选择要比较的文件，右键 👉 打开更改（或者点击文件名后的 `M` ）。

![source-control-icon.png](https://i.loli.net/2020/02/28/L3qCzkJgD47miOe.png)

**并排显示：**

默认为并排比较差异。

![git_side_by_side.png](https://i.loli.net/2020/02/28/dYlqs4Z2kiCTLe8.png)

**内联视图：**

通过单击右上角的 " **更多操作**（…）" 按钮并选择 " **切换到内联视图" ** 来 **切换内联视图** 。

![git_inline.png](https://i.loli.net/2020/02/28/qK8EDO1FaVChGAU.png)

如果您喜欢嵌入式视图，可以设置`"diffEditor.renderSideBySide": false`。

**审查窗格**

使用 F7 和 `Shift + F7` 浏览差异。这将以统一的补丁格式显示它们。可以使用箭头键浏览行，然后按 Enter 键将在差异编辑器和所选行中跳回。

![diff_review_pane.png](https://i.loli.net/2020/02/28/OjGgFhvTatfwsIP.png)

**编辑待定更改**

您可以直接在 diff 视图的未决更改中进行编辑

### Branches 分支

通过状态栏轻松在 Git 分支之间切换。

![switch_branches.gif](https://i.loli.net/2020/02/28/iLMEy9Ngz1WGvDh.gif)

### Staging 暂存

暂存所有：

![git_stage_all.gif](https://i.loli.net/2020/02/28/itkGxyu7v4U1FDw.gif)

暂存文件中的部分内容：

通过选择文件（使用箭头），然后从" 命令面板" 中 选择 " 暂存选定范围"，暂存文件的一部分。

### 撤销上一次提交

![undo_last_commit.gif](https://i.loli.net/2020/02/28/YNVcO6oMzqZimI8.gif)

### 查看 Git 输出

VS Code 使得查看实际运行的 Git 命令变得容易。当学习 Git 或调试困难的源代码控制问题时，这很有用。

使用**切换输出**命令（`Ctrl + Shift + U`），然后在下拉菜单中选择**Git**。

### Gutter 指示符

边槽指示器

![Gutter 指示器](https://code.visualstudio.com/assets/docs/getstarted/tips-and-tricks/editingevolved_gutter.png)

如果打开的文件夹是 Git 存储库并开始进行更改，则 VS Code 将在装订线和概览标尺中添加有用的注释。

- 红色三角形表示已删除行的位置
- 绿色条表示新添加的行
- 蓝色条表示已修改的行

### 解决合并冲突

在合并期间，转到 " **源代码控制"** 视图（`Ctrl + Shift + G`），然后在 diff 视图中进行更改。

### 更多配置

将 VS Code 设置为默认合并工具

```
git config --global merge.tool code
```



使用 VS code 作为 diff 工具



```
# 先 将 vs code 作为git的默认编辑器 git config --global core.editor "code --wait" # 用vscode 打开 .gitconfig文件 git config --global -e # 在 .gitconfig文件 中添加 [diff]    tool = default-difftool [difftool "default-difftool"]    cmd = code --wait --diff $LOCAL $REMOTE 
```

## 调试

### 配置调试器

打开 **命令面板**（`Ctrl + Shift + P`）并输入命令 `Debug: Open launch.json` ，它将提示您选择与项目（Node.js，Python，C ++等）匹配的环境，这将生成一个`launch.json`文件。Node.js 支持是内置的，其他环境要求安装适当的语言扩展。

![configure_debug.gif](https://i.loli.net/2020/02/28/YxdFgDtiuyR4pHs.gif)

和其它调试 IDE 一样，你可以查看变量、堆栈追踪，甚至对变量内容进行更改

### 断点和逐步

**断点和逐句通过**

在行号旁边放置断点。使用"调试"小部件向前导航。

![node_debug.gif](https://i.loli.net/2020/02/28/jFpxRDVnBfrLKUZ.gif)

### Data inspection（数据检查）

![debug_data_inspection.gif](https://i.loli.net/2020/02/28/QWDpUxrdJI7h5BY.gif)

### 内联值

您可以设置`"debug.inlineValues": true`为在调试器中内联查看变量值。此功能可能很昂贵，并且可能减慢步进速度，因此默认情况下禁用此功能。

## 任务执行器 Task runner

> 另可参考下文的 Task 任务

### 自动检测任务

从顶层菜单中选择**终端**，运行命令 `Configure Tasks`，然后选择您要运行的任务类型。这将生成一个`tasks.json`内容如下的文件。有关更多详细信息，请参见[任务](https://code.visualstudio.com/docs/editor/tasks)文档。

自动生成有时会出现问题。请查阅文档以确保一切正常。

### 从终端菜单运行任务

从顶层菜单中选择**Terminal(终端)**，运行命令`Run Task`，然后选择要运行的任务。通过运行命令`Terminate Task` 终止正在运行的**任务**

![task_runner.gif](https://i.loli.net/2020/02/28/Nx9e1lFYnAURu3Z.gif)

### 定义任务的键盘快捷键

您可以为任何任务定义键盘快捷键。在**命令面板**（Ctrl + Shift + P）中，选择`Preferences: Open Keyboard Shortcuts File`，将所需的快捷方式绑定到`workbench.action.tasks.runTask`命令，然后将**任务**定义为`args`。

例如，要将`Ctrl + H`绑定到`Run tests`任务，请添加以下内容：

```
{
  "key": "ctrl+h",
  "command": "workbench.action.tasks.runTask",
  "args": "Run tests"
}
```



### 将 npm 脚本作为资源管理器中的任务运行

使用该设置`npm.enableScriptExplorer`，您可以启用一个浏览器，该浏览器显示在工作空间中定义的脚本。

![script_explorer.png](https://i.loli.net/2020/02/28/gweSyrN7zFl8UPO.png)

在资源管理器中，您可以在编辑器中打开脚本，将其作为任务运行，然后使用节点调试器启动脚本（当脚本定义了诸如的调试选项时`--inspect-brk`）。单击时的默认操作是打开脚本。要单击运行脚本，请设置`npm.scriptExplorerAction`为"运行"。使用该设置`npm.exclude`可以排除`package.json`特定文件夹中包含的文件中的脚本。

通过设置`npm.enableRunFromFolder`，您可以启用从文件资源管理器的上下文菜单中为文件夹运行 npm 脚本的功能。选择文件夹后，该设置将启用命令`Run NPM Script in Folder...`。该命令显示此文件夹中包含的 npm 脚本的快速选择列表，您可以选择要作为任务执行的脚本。

## VS Code 的设置

VS Code 提供了两种不同的设置范围：

- **用户设置** -全局应用于您打开的任何 VS Code 实例的设置。
- **工作区设置** -存储在工作**区中的设置**，仅在打开工作区时适用。

工作区设置将覆盖用户设置。工作区设置特定于项目，并且可以在项目的开发人员之间共享。

工作区设置以及[调试](https://code.visualstudio.com/docs/editor/debugging)和[任务](https://code.visualstudio.com/docs/editor/tasks)配置存储在`.vscode`文件夹的根目录中。通过称为" [多根工作区"](https://code.visualstudio.com/docs/editor/multi-root-workspaces)的功能，VS Code 工作区中还可以具有多个根文件夹。

> 工作区文件夹在 **.vscode** 中 的`tasks.json`用于任务运行，`launch.json`用于调试器。

默认情况下，VS Code 显示"设置"编辑器，但是您仍然可以`settings.json`通过使用`Open Settings (JSON)`命令 或 通过使用设置更改默认设置编辑器来编辑基础文件`workbench.settings.editor`。

> 打开用户设置 `settings.json` 文件，你可以通过（命令面板）输入命令：`Open Settings (JSON)` 来打开此文件。

**配置特定于语言的设置**：

要按（编程）语言自定义编辑器，请从**命令面板**（Ctrl + Shift + P）中运行全局命令 `Configure Language Specific Settings` ，这将打开语言选择器。选择所需的语言，打开带有语言条目的"设置"编辑器，您可以在其中添加适用的设置。

（还可以是特定文件类型的配置）如果您打开了一个文件，并且想要为此文件类型自定义编辑器，请在" VS 代码"窗口右下方的状态栏中单击"语言模式"。这将打开"语言模式"选择器，并带有一个选项" **配置基于语言的语言的设置"**。选择此项将打开带有语言条目的"设置"编辑器，您可以在其中添加适用的设置。

以下示例自定义语言模式`typescript`和的编辑器设置`markdown` ：



```
{  "[typescript]": {    "editor.formatOnSave": true,    "editor.formatOnPaste": true  },  "[markdown]": {    "editor.formatOnSave": true,    "editor.wordWrap": "on",    "editor.renderWhitespace": "all",    "editor.acceptSuggestionOnEnter": "off"  } } 
```

## Task 任务

> [Visual Studio Code 中的任务](https://code.visualstudio.com/Docs/editor/tasks#_processing-task-output-with-problem-matchers)

> 看起来就像是为了更方便的让我们执行需要在终端运行的命令，你看它位于 菜单 👉 终端下

许多插件可以自动执行诸如整理，构建，打包，测试或部署软件系统之类的任务 ，但安装这些插件后，在对应的工程中，它们会提供一些默认的任务。（对于 maven 的任务现在正在开发中）。我们可以通过快捷键`Ctrl + Shift + B`或终端菜单来列出这些任务。

任务有全局的也有仅用于当前工作空间的（它在项目的.vscode 目录下）

当然你可以自定义任务（为该工程手动创建一个任务）：

菜单 👉 终端 👉 配置任务 👉 选择创建 task.json 文件 👉 它会提供几个模板，如果模板中没有则选择 Others。



```
{  // See https://go.microsoft.com/fwlink/?LinkId=733558  // for the documentation about the tasks.json format  "version": "2.0.0",  "tasks": [    {      "label": "Run tests",  //任务名称      "type": "shell",    //任务类型：shell（命令）或process      "command": "./scripts/test.sh",  //实际要执行的命令      "windows": {  //如果在win中则优先使用下面的内容        "command": ".\\scripts\\test.cmd"      },      "group": "test", //任务所属的 组      "presentation": { //定义如何在用户界面中处理输出         //下面表示每次执行任务都让其创建一个新的终端        "reveal": "always",        "panel": "new"      }        "options":        "runOptions":    },    {        "label": "Client Build",        "type":"shell",        "command": "gulp",        "args": ["build"], //参数        "options": { //覆盖 cwd(当前工作目录)、env(环境变量)、shell(默认shell)的值        "cwd": "${workspaceRoot}/client"      }    }  ] } 
```

另外还有：(使用 ctrl+space 触发提示)

- options：覆盖 cwd(当前工作目录)、env(环境变量)、shell(默认 shell)的值
- runOptions： 定义何时以及如何运行任务
- args：命令的参数 示例 `"args":["folder"]`

对于包含空格或其他特殊字符的命令和参数，Shell 命令需要特殊对待

- 如果提供单个命令，那么任务系统会将命令原样传递给底层 shell。如果命令需要加引号或转义才能正常运行，则该命令需要包含正确的引号或转义字符。例如，要列出包含空格的名称中的文件夹的目录，命令在 bash 执行应该是这样的：`ls 'folder with spaces'`。

  

- `{  "label": "dir",  "type": "shell",  "command": "dir 'folder with spaces'" } `
- 如果提供了命令和参数，则如果命令或参数包含空格，则任务系统将使用单引号。对于`cmd.exe`，使用双引号。如下所示的 shell 命令将在 PowerShell 中以方式执行`dir 'folder with spaces'`。



```
{  "label": "dir",  "type": "shell",  "command": "dir",  "args": ["folder with spaces"] } 
```

- 如果要控制如何对参数加引号，则参数可以是指定值和引用样式的文字。下面的示例使用转义而不是使用空格引号。



```
{  "label": "dir",  "type": "shell",  "command": "dir",  "args": [    {      "value": "folder with spaces",      "quoting": "escape"    }  ] } 
```

> 可更改默认终端为 cmd 、bash 等

**控制输出行为：**

同设置 `presentation` 的属性来控制终端行为，有如下属性：

- **reveal** ：控制是否将集成终端面板置于前面。有效值为：
- always - 面板总是放在最前面。这是默认值。
- *never* - 用户必须使用" **视图"** >" **终端"**命令（Ctrl +`）将终端面板显式显示在最前面 。
- *silent* - 仅在不扫描输出中是否有错误和警告的情况下，才将终端面板置于前面。
- **focus**：控制终端是否获取输入焦点。默认值为`false`。
- **echo**：控制是否在终端中回显执行的命令。默认值为`true`。
- **showReuseMessage**：控制是否显示"终端将被任务重用，请按任意键将其关闭"消息。
- panel：控制是否在任务运行之间共享终端实例。可能的值为：
  - *shared*：*共享*终端，并将其他任务运行的输出添加到同一终端。
  - *dedicated*：终端专用于特定任务。如果再次执行该任务，则将重新使用终端。但是，不同任务的输出将显示在不同终端中。
  - *new*：该任务的每次执行都使用新的干净终端。
- **clear**：控制在运行此任务之前是否清除终端。默认值为`false`。
- **group**：控制是否使用拆分窗格在特定的终端组中执行任务。同一组中的任务（由字符串值指定）将使用拆分终端显示，而不是新的终端面板。

## 下一步

继续阅读以了解以下内容：

- [代码导航](https://code.visualstudio.com/docs/editor/editingevolved) -窥视和转到定义等。
- [集成终端](https://code.visualstudio.com/docs/editor/integrated-terminal) -了解用于在 VS Code 中快速执行命令行任务的集成终端。
- [IntelliSense](https://code.visualstudio.com/docs/editor/intellisense) -VS Code 带来了智能代码补全功能。
- [调试](https://code.visualstudio.com/docs/editor/debugging) -这是 VS Code 真正发挥作用的地方

## 学习文档

[Documentation for Visual Studio Code](https://code.visualstudio.com/docs)

[VScode 中文文档](https://www.gitbook.com/book/jeasonstudio/vscode-cn-doc/details)

[VS Code Tips and Tricks](https://github.com/Microsoft/vscode-tips-and-tricks)

[Visual Studio Code 配置指南](https://github.com/kaiye/kaiye.github.com/issues/14)

[Key Bindings for Visual Studio Code](https://github.com/kaiye/kaiye.github.com/issues/14)

也可以查看 VS Code 的自带帮助，来学习它。比如： `帮助 --> 欢迎使用`

[Visual Studio Code User and Workspace Settings](https://code.visualstudio.com/docs/getstarted/settings)

[Microsoft/vscode-tips-and-tricks: Collection of helpful tips and tricks for VS Code.](https://github.com/Microsoft/vscode-tips-and-tricks)

​    您的鼓励是我最大的动力  

​            

​          

------

​                      ![Felix](data:image/svg+xml,%0A%3Csvg xmlns='http://www.w3.org/2000/svg' width='24' height='24' viewBox='0 0 24 24'%3E%3Cpath fill='none' d='M0 0h24v24H0V0z'/%3E%3Cpath fill='%23aaa' d='M19 3H5c-1.1 0-2 .9-2 2v14c0 1.1.9 2 2 2h14c1.1 0 2-.9 2-2V5c0-1.1-.9-2-2-2zm-1 16H6c-.55 0-1-.45-1-1V6c0-.55.45-1 1-1h12c.55 0 1 .45 1 1v12c0 .55-.45 1-1 1zm-4.44-6.19l-2.35 3.02-1.56-1.88c-.2-.25-.58-.24-.78.01l-1.74 2.23c-.26.33-.02.81.39.81h8.98c.41 0 .65-.47.4-.8l-2.55-3.39c-.19-.26-.59-.26-.79 0z'/%3E%3C/svg%3E)            

​      作者    

​              Felix          

​              如无必要，勿增实体。          

​                                          [         ](mailto:fandean@outlook.com)

[       ](mailto:fandean@outlook.com)[           ](https://github.com/fandean)[          ](https://github.com/fandean)[         ](https://www.jianshu.com/u/b87e72c5bb90)[       ](https://www.jianshu.com/u/b87e72c5bb90)[         ](https://t.me/fandean)[       ](https://t.me/fandean)[         ](https://www.zhihu.com/people/fandean)

[       ](https://www.zhihu.com/people/fandean)                

------

#                     相关内容                

- ​          [VS Code中进行Java开发(1)：配置开发环境](https://www.thisfaner.com/p/vs-code-jdk-configure/)        
- ​          [VS Code中进行Java开发(2)：代码编辑](https://www.thisfaner.com/p/vs-code-skills/)        
- ​          [VS Code中进行Java开发(3)：maven 项目管理](https://www.thisfaner.com/p/vs-code-maven/)        
- ​          [VS Code中进行Java开发(4)：运行和调试](https://www.thisfaner.com/p/vs-code-java-debug/)        

​          

ImageMagick命令

VS Code中进行Java开发(4)：运行和调试

​          

 3449









1 评论

![img](https://gravatar.loli.net/avatar/d41d8cd98f00b204e9800998ecf8427e?d=robohash&v=1.5.2)

Anonymous Edge 85.0.564.51 Windows 10/11

2020-09-21回复

厉害！

Powered By [Valine](https://valine.js.org)
v1.5.2

​                                                [         ](mailto:fandean@outlook.com)

[       ](mailto:fandean@outlook.com)[           ](https://github.com/fandean)[          ](https://github.com/fandean)[         ](https://www.jianshu.com/u/b87e72c5bb90)[       ](https://www.jianshu.com/u/b87e72c5bb90)[         ](https://t.me/fandean)[       ](https://t.me/fandean)[         ](https://www.zhihu.com/people/fandean)[       ](https://www.zhihu.com/people/fandean)[         ](https://www.thisfaner.com/posts//index.xml)

[       ](https://www.thisfaner.com/posts//index.xml)         

​      

------

​            

​                

​                                                                                                     除非另有声明，本网站内容采用[CC BY-NC-SA 4.0 ](https://creativecommons.org/licenses/by-nc-sa/4.0/deed.zh)授权                                                

Powered by [Hugo](https://gohugo.io/) and the [Zzo theme](https://github.com/zzossig/hugo-theme-zzo)

###### 目录

​                                  

















#### 快捷大全

