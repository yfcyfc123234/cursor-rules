# Cursor 项目规则自动化管理系统

> 一个智能的 Cursor IDE 项目规则管理系统，支持从 GitHub 或本地缓存自动拉取规则，根据项目类型自动匹配，实现规则的一键导入和自动化管理。

## 📋 项目概述

本项目旨在实现一个智能的 Cursor 项目规则自动化管理系统。当你打开或新建一个 Cursor 项目时，系统能够：

- 🔍 **自动检测项目类型**：识别 Android、Flutter、Python、PHP 等项目类型
- 📥 **自动拉取规则**：从 GitHub 仓库或本地缓存文件夹获取对应的规则文件
- 🎯 **智能匹配规则**：根据项目类型自动匹配并导入相应的规则
- 🚀 **一键导入**：支持用户通过自然语言指令触发规则导入
- 🎨 **UI 设计还原**：支持蓝湖设计图的一比一像素还原规则

## 🎯 核心功能

### 1. 项目类型自动检测

系统能够自动识别以下项目类型：

- **Flutter 混合项目**：存在 `pubspec.yaml` 且存在 `android/` 目录
- **Flutter 项目**：存在 `pubspec.yaml`
- **Android 项目**：存在 `settings.gradle` 或根目录 `build.gradle`
- **Python 项目**：存在 `requirements.txt` 或 `pyproject.toml`
- **PHP 项目**：存在 `composer.json`
- **Kotlin/Java 项目**：根据主要代码文件类型判断

### 2. 规则自动拉取

#### 规则来源

- **GitHub 仓库**：`https://github.com/yfcyfc123234/cursor-rules`
- **本地缓存**：`C:\Users\Administrator\Desktop\cursor-rules`

#### 拉取策略

1. **优先从本地缓存拉取**：如果本地存在规则文件，直接使用
2. **GitHub 作为备用**：本地不存在时从 GitHub 拉取
3. **自动更新缓存**：从 GitHub 拉取成功后更新本地缓存

### 3. 规则文件分类

#### 通用规则（Common Rules）

位于 `common-rules/` 目录，适用于所有项目：

- `user-base-rule.mdc` - 用户基础规则（个人偏好、沟通风格等）
- `git-automation.mdc` - Git 自动化规则
- `auto-import-rules.mdc` - 规则自动导入规则
- `ui-design-reconstruction.mdc` - UI 设计图还原规则
- `project-rules-auto-management.mdc` - 项目规则管理规则
- `batch-file-operations.mdc` - 批量文件操作优化规则
- `github-rules-sync.mdc` - GitHub 同步规则

#### 项目规则（特定规则）

位于根目录，根据项目类型匹配：

- `android-project.mdc` - Android 项目规则
- `flutter-project.mdc` - Flutter 项目规则
- `android-flutter-project.mdc` - Android+Flutter 混合项目规则
- `python-project.mdc` - Python 项目规则
- `php-project.mdc` - PHP 项目规则
- `kotlin-project.mdc` - Kotlin 项目规则
- `java-project.mdc` - Java 项目规则

### 4. 触发机制

#### 自动触发

- **打开项目时**：检测到 `.cursor/rules/` 目录为空时自动执行
- **提示模式**：自动检测后提示用户确认是否导入

#### 手动触发

支持以下自然语言指令：

**导入规则**：
- "导入规则"
- "帮我导入规则"
- "导入安卓规则"
- "导入 Flutter 规则"
- "这是 Flutter 项目，导入规则"
- "这是一个 Android 项目"

**更新规则**：
- "更新规则"
- "同步规则"
- "刷新规则"
- "重新导入规则"
- 当规则项目数据发生变化时，使用这些指令更新当前项目的规则文件

### 5. 蓝湖 UI 设计图还原

当用户提供蓝湖 UI 设计图（效果图 + 切图）时：

- **自动识别**：AI 自动识别图片中的设计元素和尺寸
- **一比一还原**：尽量按照设计图一比一还原页面
- **沉浸式栏处理**：针对 APP 项目的沉浸式状态栏进行特殊处理
- **用户补充**：支持用户补充描述，AI 根据描述和图片还原

## 📁 项目结构

```
cursor-rules/
├── README.md                          # 项目说明文档（本文件）
├── common-rules/                       # 通用规则（适用于所有项目）
│   ├── user-base-rule.mdc             # 用户基础规则
│   ├── git-automation.mdc             # Git 自动化规则
│   ├── auto-import-rules.mdc          # 规则自动导入规则
│   ├── ui-design-reconstruction.mdc   # UI 设计图还原规则
│   ├── project-rules-auto-management.mdc  # 项目规则管理规则
│   ├── batch-file-operations.mdc      # 批量文件操作优化规则
│   └── github-rules-sync.mdc          # GitHub 同步规则
├── android-project.mdc                # Android 项目规则
├── flutter-project.mdc                # Flutter 项目规则
├── android-flutter-project.mdc       # Android+Flutter 混合项目规则
├── python-project.mdc                 # Python 项目规则
├── php-project.mdc                    # PHP 项目规则
├── kotlin-project.mdc                 # Kotlin 项目规则
└── java-project.mdc                   # Java 项目规则
```

## 🚀 使用方法

### 场景 1：打开新项目

当你打开一个新的 Cursor 项目时：

1. 系统自动检测项目类型
2. 如果 `.cursor/rules/` 目录为空，自动提示是否导入规则
3. 确认后自动从 GitHub 或本地缓存拉取规则
4. 规则文件自动保存到 `.cursor/rules/` 目录

### 场景 2：手动导入规则

在 Cursor 中与 AI 对话：

```
用户：帮我导入规则
AI：检测到这是一个 Flutter 项目，正在从 GitHub 拉取规则...
AI：✅ 已成功导入规则文件到 .cursor/rules/ 目录
```

### 场景 3：指定项目类型

在空白文件夹中：

```
用户：这是一个 Flutter 项目，导入规则
AI：正在为 Flutter 项目导入规则...
AI：✅ 已成功导入 Flutter 项目规则
```

### 场景 4：使用蓝湖设计图

```
用户：[上传蓝湖设计图]
用户：帮我根据这个设计图还原页面，这是沉浸式栏的 APP 项目
AI：正在分析设计图，将按照一比一像素还原...
```

## 🔧 配置说明

### GitHub 仓库配置

- **仓库地址**：`https://github.com/yfcyfc123234/cursor-rules`
- **默认分支**：`main`
- **Raw Content URL**：`https://raw.githubusercontent.com/yfcyfc123234/cursor-rules/main/`

### 本地缓存路径

- **Windows**：`C:\Users\Administrator\Desktop\cursor-rules`
- 如需修改，可在规则文件中更新路径配置

## 📝 规则文件格式

所有规则文件必须包含 frontmatter 元数据：

```markdown
---
alwaysApply: true
---

# 规则标题

规则内容...
```

## 🔄 工作流程

### 规则导入流程

1. **触发检测**
   - 检测 `.cursor/rules/` 目录状态
   - 识别用户指令或自动触发

2. **项目类型识别**
   - 自动检测项目类型
   - 支持用户明确指定

3. **规则来源选择**
   - 优先从本地缓存拉取
   - 本地不存在时从 GitHub 拉取

4. **规则文件拉取**
   - 拉取通用规则（`common-rules/` 目录）
   - 拉取项目规则（根据项目类型）

5. **文件验证和处理**
   - 验证 frontmatter 格式
   - 处理文件名冲突（使用递增后缀）

6. **保存到项目**
   - 创建 `.cursor/rules/` 目录
   - 保存所有规则文件

7. **完成提示**
   - 显示成功导入的规则文件列表

## 🎨 蓝湖 UI 设计图还原规则

### 核心要求

1. **一比一像素还原**
   - 严格按照设计图的尺寸、颜色、字体、间距还原
   - 使用精确的像素值，避免近似值

2. **沉浸式状态栏处理**
   - APP 项目通常使用沉浸式状态栏
   - 状态栏颜色与页面背景色一致
   - 内容区域需要考虑状态栏高度

3. **切图资源使用**
   - 优先使用提供的切图资源
   - 切图命名规范，便于引用
   - 考虑不同屏幕密度的适配

4. **响应式适配**
   - 在保证设计还原的前提下，考虑不同屏幕尺寸
   - 使用相对单位（dp、sp）而非固定像素
   - 关键元素保持设计图比例

### 处理流程

1. **设计图分析**
   - AI 自动识别设计图中的元素
   - 提取颜色、字体、尺寸、间距等信息

2. **用户补充**
   - 支持用户补充描述（如特殊交互、动画效果等）
   - AI 结合设计图和用户描述进行还原

3. **代码生成**
   - 生成符合项目规范的代码
   - 确保代码可运行、可维护

## 🔍 项目类型检测逻辑

### 检测优先级

1. **Flutter 混合项目**
   - 条件：`pubspec.yaml` + `android/` 目录
   - 规则：`android-flutter-project.mdc`

2. **Flutter 项目**
   - 条件：`pubspec.yaml`
   - 规则：`flutter-project.mdc`

3. **Android 项目**
   - 条件：`settings.gradle` 或 `build.gradle`，且无 `pubspec.yaml`
   - 规则：`android-project.mdc`

4. **Python 项目**
   - 条件：`requirements.txt` 或 `pyproject.toml`
   - 规则：`python-project.mdc`

5. **PHP 项目**
   - 条件：`composer.json`
   - 规则：`php-project.mdc`

6. **其他类型**
   - 根据主要代码文件类型判断
   - `.kt` 文件为主 → `kotlin-project.mdc`
   - `.java` 文件为主 → `java-project.mdc`

## 📋 待实现功能

### 当前状态

- ✅ 项目类型自动检测
- ✅ GitHub 规则拉取
- ✅ 本地缓存支持
- ✅ 规则文件自动导入
- ✅ 用户指令识别
- ⚠️ 蓝湖 UI 设计图还原规则（需要进一步完善）

### 未来优化方向

1. **规则版本管理**
   - 支持规则文件版本控制
   - 规则更新通知机制

2. **多仓库支持**
   - 支持配置多个 GitHub 仓库
   - 支持私有仓库（需要认证）

3. **规则模板系统**
   - 支持自定义规则模板
   - 规则模板市场

4. **规则冲突处理**
   - 智能合并规则冲突
   - 规则优先级管理

5. **性能优化**
   - 规则文件缓存机制
   - 增量更新支持

## 🤝 贡献指南

### 如何添加新的项目类型规则

1. 在根目录创建新的规则文件，如 `react-project.mdc`
2. 在 `project-rules-auto-management.mdc` 中添加项目类型检测逻辑
3. 在 `github-rules-sync.mdc` 中添加项目类型映射
4. 更新本 README 文档

### 如何优化现有规则

1. 直接编辑对应的 `.mdc` 文件
2. 确保包含完整的 frontmatter
3. 遵循现有的规则文件格式
4. 提交到 GitHub 仓库

## 📚 相关文档

- [Cursor Rules 官方文档](https://cursor.sh/docs)
- [GitHub 仓库](https://github.com/yfcyfc123234/cursor-rules)

## 📄 许可证

本项目采用 MIT 许可证。

## 💡 使用建议

1. **首次使用**：建议先手动导入一次规则，熟悉流程
2. **规则更新**：定期从 GitHub 同步最新规则
3. **自定义规则**：可以在项目本地 `.cursor/rules/` 目录添加项目特定规则
4. **规则优先级**：项目规则 > 通用规则（项目特定规则优先）

## 🐛 问题反馈

如遇到问题，请：

1. 检查网络连接（GitHub 拉取需要网络）
2. 检查规则文件格式（必须包含 frontmatter）
3. 检查项目类型检测是否正确
4. 在 GitHub 仓库提交 Issue

---

**最后更新**：2025-01-27

**维护者**：yfcyfc123234

