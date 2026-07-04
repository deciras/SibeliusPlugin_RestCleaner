# RestCleaner for Sibelius

[中文](#中文说明) | [English](#english)

---

# 中文说明

## 简介

RestCleaner 是一个用于 **Sibelius** 的插件，用于自动整理乐谱中的休止符，使其更符合常见的出版级记谱规则。

这个插件主要用于修复两类常见问题：

1. **非法跨拍休止符**  
   例如在 4/4 拍中，一个四分休止符横跨拍子边界，这种写法通常不符合规范。

2. **未按记谱规则合并的连续休止符**  
   例如本应合并的两个十六分休止符、两个八分休止符，或符合规则的两个四分休止符。

---

## 当前功能

当前版本（v1.3.0）主要支持以下功能：

### 1. 修复非法跨组四分休止符

插件会按当前**所在小节的拍号**判断一个四分休止符是否跨越了不该跨越的节拍组边界；如果跨越，插件会将其拆分为更合适的休止符写法。

例如：

- 不规范：跨越拍边界的四分休止符
- 规范：两个八分休止符

### 2. 迭代合并合法连续休止符

插件会在符合出版级规则的前提下合并相邻休止符，并持续迭代，直到当前选区里不再出现新的合法合并。例如：

- 十六分休止符 + 十六分休止符 → 八分休止符
- 八分休止符 + 八分休止符 → 四分休止符（仅限同一节拍组内）
- 四分休止符 + 四分休止符 → 二分休止符（仅限当前拍号允许的组内位置）

### 3. 避免错误合并

插件会尽量避免以下不符合规范的合并：

- 跨拍边界的八分休止符合并成四分休止符
- 在 4/4 中将第 2 拍与第 3 拍的四分休止符合并成二分休止符
- 破坏节拍结构可读性的合并

### 4. GUI 设置窗口

运行插件后会先弹出一个设置窗口，你可以在里面：

- 选择只做“修复非法休止符”或只做“合并合法休止符”
- 选择“仅检测不修改”
- 查看当前选区里检测到的拍号
- 为奇数 `x/8` 拍号输入本次运行要使用的重音分组

---

## 当前支持情况

当前版本会**逐小节读取当前拍号**，所以在同一段选区内遇到变拍时，也会按每个小节分别判断，而不是把第一个拍号套用到整段音乐。

目前已实现的重点支持包括：

- `2/4`
- `3/4`
- `4/4`
- `6/8`

另外，对以下奇数 `x/8` 拍号支持**运行时自定义分组**：

- `5/8`
- `7/8`
- `11/8`
- `13/8`

说明：

- 对分母为 `4` 的拍号，插件按四分拍分组处理。
- 对 `6/8` 这类复拍子，插件按附点四分拍分组处理。
- 对 `5/8`、`7/8`、`9/8`、`11/8`、`13/8`，你可以在 GUI 里直接输入分组，例如 `2+3`、`3+2`、`2+2+3`、`3+3+3`。
- 如果当前选区没有出现某个奇数拍号，对应输入不会参与本次运行。
- 对未单独提供输入框的其他奇数 `x/8` 拍号，插件仍会使用默认分组策略。

---

## 安装方法

请下载插件文件：

`RestCleaner.plg`

然后将其复制到 Sibelius 的用户插件目录中。

### Windows

`C:\Users\<用户名>\AppData\Roaming\Avid\Sibelius\Plugins\`

### macOS

`~/Library/Application Support/Avid/Sibelius/Plugins/`

你也可以在 `Plugins` 目录下新建一个子文件夹，例如：

`Plugins/Rest Cleaner/`

安装完成后，请**重新启动 Sibelius**。

---

## 使用方法

1. 在乐谱中**框选需要处理的区域**（passage selection）
2. 在 Sibelius 中运行插件：

`Plugins → Rest Cleaner → RestCleaner`

插件会先弹出 GUI 设置窗口；确认后再按顺序执行：

1. 修复非法休止符
2. 合并合法休止符

---

## 使用建议

在运行插件之前，建议：

- 先保存乐谱
- 或先在副本上测试

如果结果不符合预期，可以使用撤销：

- macOS：`Cmd + Z`
- Windows：`Ctrl + Z`

---

## 已知限制

当前版本仍有一些限制：

- 暂未完整区分不同声部（Voice）
- 对复杂 Tuplet / 三连音情况支持有限
- “仅检测不修改”模式下，合并数量只基于当前状态估计，不继续模拟后续迭代
- 未单独提供输入框的其他奇数 `x/8` 拍号仍使用默认分组，不一定匹配所有作品的真实重音结构
- 建议先在简单、单声部或较清晰的谱面上测试，再应用到复杂总谱

---

## 项目结构

```text
SibeliusPlugin_RestCleaner/
├─ RestCleaner.plg
├─ README.md
├─ LICENSE
├─ CHANGELOG.md
└─ VERSION
```

---

## 未来计划

未来版本可能增加：

- 更严格的出版级休止符规则
- 声部感知处理
- 更完整的奇数拍覆盖范围
- 更细的“仅检测”预估逻辑

---

## 许可证

本项目采用 **MIT License**。

---

## 作者

作者：**Deciras**

如果你发现问题，或对插件有改进建议，欢迎提交 Issue。

---

# English

## Overview

RestCleaner is a **Sibelius** plugin designed to clean and normalize rests according to common engraving rules.

It mainly addresses two types of problems:

1. **Illegal cross-beat rests**  
   For example, in 4/4 meter, a quarter rest that crosses a beat boundary is usually not considered proper notation.

2. **Adjacent rests that should be merged but are not**  
   For example, two sixteenth rests, two eighth rests, or two quarter rests that should be merged according to engraving rules.

---

## Current Features

Current version (v1.3.0) mainly provides the following features:

### 1. Fix illegal cross-group quarter rests

The plugin reads the **meter of the current bar** and rewrites quarter rests that cross a beat-group boundary that should stay visible.

For example:

- Incorrect: one quarter rest crossing a beat boundary
- Correct: two eighth rests

### 2. Iteratively merge legal adjacent rests

The plugin merges adjacent rests only when the result follows engraving-style rules, and keeps iterating until no further legal merge remains in the current selection. For example:

- sixteenth rest + sixteenth rest → eighth rest
- eighth rest + eighth rest → quarter rest (only within the same beat group)
- quarter rest + quarter rest → half rest (only where the current meter/grouping allows it)

### 3. Avoid incorrect merges

The plugin tries to avoid merges that would hide beat structure, such as:

- merging eighth rests across a beat boundary into a quarter rest
- merging quarter rests across beats 2–3 in 4/4 into a half rest
- merges that reduce rhythmic readability

### 4. GUI options dialog

Before processing, the plugin now opens a small dialog where you can:

- run only the split step or only the merge step
- choose a detect-only mode
- review which meters were found in the current selection
- enter the grouping to use for odd `x/8` meters in this run

---

## Current Support

The current version processes the selection **bar by bar**, so mixed-meter passages are handled using the local meter of each bar rather than one global assumption.

Implemented focus meters include:

- `2/4`
- `3/4`
- `4/4`
- `6/8`

The plugin supports **runtime grouping input** for odd `x/8` meters such as:

- `5/8`
- `7/8`
- `11/8`
- `13/8`

Notes:

- For denominator-`4` meters, the plugin uses quarter-note beat groups.
- For `6/8`-style compound meters, the plugin uses dotted-quarter beat groups.
- For `5/8`, `7/8`, `9/8`, `11/8`, and `13/8`, you can enter a grouping such as `2+3`, `2+2+3`, or `3+3+3` in the GUI.
- If a given odd meter does not appear in the current selection, its input is ignored for that run.
- Other odd `x/8` meters without dedicated input fields still fall back to the default grouping strategy.

---

## Installation

Download the plugin file:

`RestCleaner.plg`

Then copy it to your Sibelius user plugin directory.

### Windows

`C:\Users\<username>\AppData\Roaming\Avid\Sibelius\Plugins\`

### macOS

`~/Library/Application Support/Avid/Sibelius/Plugins/`

You may also create a subfolder inside `Plugins`, for example:

`Plugins/Rest Cleaner/`

After installation, **restart Sibelius**.

---

## Usage

1. Make a **passage selection** in your score
2. Run the plugin in Sibelius:

`Plugins → Rest Cleaner → RestCleaner`

The plugin first opens the GUI dialog; after confirmation, it runs in this order:

1. fix illegal rests
2. merge legal rests

---

## Recommendations

Before running the plugin, it is recommended to:

- save your score first
- or test it on a copy

If needed, you can always undo:

- macOS: `Cmd + Z`
- Windows: `Ctrl + Z`

---

## Known Limitations

The current version still has several limitations:

- it does not yet fully distinguish voices
- support for complex tuplets is limited
- detect-only mode estimates merge opportunities from the current notation state and does not fully simulate later iterative passes
- odd `x/8` meters without dedicated input fields still use the default grouping fallback
- testing on relatively clear single-voice or simple textures is still recommended first

---

## Project Structure

```text
SibeliusPlugin_RestCleaner/
├─ RestCleaner.plg
├─ README.md
├─ LICENSE
├─ CHANGELOG.md
└─ VERSION
```

---

## Roadmap

Possible future improvements include:

- stricter engraving-level rest rules
- voice-aware processing
- broader odd-meter coverage
- finer detect-only estimation

---

## License

This project is released under the **MIT License**.

---

## Author

Author: **Deciras**

If you find a bug or have suggestions for improvement, feel free to open an Issue.
