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

当前版本（v1.0）主要支持以下功能：

### 1. 修复非法跨拍四分休止符

在 4/4 拍中，如果一个四分休止符起始于错误的位置、横跨拍边界，插件会将其拆分为更合适的休止符写法。

例如：

- 不规范：跨越拍边界的四分休止符
- 规范：两个八分休止符

### 2. 合并合法连续休止符

插件会在符合出版级规则的前提下合并相邻休止符，例如：

- 十六分休止符 + 十六分休止符 → 八分休止符
- 八分休止符 + 八分休止符 → 四分休止符（仅限同一拍内）
- 四分休止符 + 四分休止符 → 二分休止符（仅限 4/4 中的第 1–2 拍或第 3–4 拍）

### 3. 避免错误合并

插件会尽量避免以下不符合规范的合并：

- 跨拍边界的八分休止符合并成四分休止符
- 在 4/4 中将第 2 拍与第 3 拍的四分休止符合并成二分休止符
- 破坏节拍结构可读性的合并

---

## 当前支持情况

目前主要针对 **4/4 拍** 进行了测试与优化。

其他拍号（如 3/4、6/8）已经进行了规则设计，但当前版本尚未完整实现或充分测试。

计划后续支持：

- 3/4
- 6/8
- 自动识别拍号
- 更严格的声部处理

---

## 安装方法

请下载插件文件：

`plugin/RestCleaner.plg`

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

插件会按顺序执行：

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

- 主要针对 4/4 拍
- 暂未完整区分不同声部（Voice）
- 对复杂 Tuplet / 三连音情况支持有限
- 建议先在简单、单声部或较清晰的谱面上测试

---

## 项目结构

```text
RestCleaner/
├─ README.md
├─ LICENSE
├─ CHANGELOG.md
└─ plugin/
   └─ RestCleaner.plg
```

---

## 未来计划

未来版本可能增加：

- 自动识别拍号
- 完整支持 3/4 与 6/8
- 更严格的出版级休止符规则
- 声部感知处理
- “仅检测、不修改”模式
- 更友好的插件参数界面

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

Current version (v1.0) mainly provides the following features:

### 1. Fix illegal cross-beat quarter rests

In 4/4 meter, if a quarter rest starts at an incorrect position and crosses a beat boundary, the plugin rewrites it into a more appropriate rest pattern.

For example:

- Incorrect: one quarter rest crossing a beat boundary
- Correct: two eighth rests

### 2. Merge legal adjacent rests

The plugin merges adjacent rests only when the result follows engraving-style rules, for example:

- sixteenth rest + sixteenth rest → eighth rest
- eighth rest + eighth rest → quarter rest (only within the same beat)
- quarter rest + quarter rest → half rest (only across beats 1–2 or 3–4 in 4/4)

### 3. Avoid incorrect merges

The plugin tries to avoid merges that would hide beat structure, such as:

- merging eighth rests across a beat boundary into a quarter rest
- merging quarter rests across beats 2–3 in 4/4 into a half rest
- merges that reduce rhythmic readability

---

## Current Support

The current version is mainly tested and optimized for **4/4** meter.

Other meters such as 3/4 and 6/8 have been planned at the rule-design level, but are not yet fully implemented or thoroughly tested.

Planned future support includes:

- 3/4
- 6/8
- automatic meter detection
- more robust voice-aware processing

---

## Installation

Download the plugin file:

`plugin/RestCleaner.plg`

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

The plugin will run in this order:

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

- mainly optimized for 4/4
- does not yet fully distinguish voices
- limited support for complex tuplets
- best tested on relatively clear single-voice or simple textures

---

## Project Structure

```text
RestCleaner/
├─ README.md
├─ LICENSE
├─ CHANGELOG.md
└─ plugin/
   └─ RestCleaner.plg
```

---

## Roadmap

Possible future improvements include:

- automatic meter detection
- full support for 3/4 and 6/8
- stricter engraving-level rest rules
- voice-aware processing
- a “detect only” mode
- a more user-friendly options dialog

---

## License

This project is released under the **MIT License**.

---

## Author

Author: **Deciras**

If you find a bug or have suggestions for improvement, feel free to open an Issue.
