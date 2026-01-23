# 小说创作系统工作流规范 (Novel Creation System Workflow)

本文档详细定义了本项目的创作工作流，包括核心文档架构、标准作业程序 (SOP) 及关键提示词策略。

## 1. 核心文档架构 (Core Documentation Architecture)

本系统采用“三层记忆模型”来管理创作上下文。

### 1.1 静态知识库 (Static Knowledge / Long-term Memory)
*   **存放位置**: `01_World_Bible/`, `02_Characters/`, `00_System_Prompts/`
*   **关键文档**:
    *   `World_Rules_Physics.md`: 世界物理法则与异能设定（不可违背的公理）。
    *   `Char_*.md`: 人物档案（包含性格关键词、内驱力、核心冲突）。
    *   `Style_Guide.md`: 文风指南（赛博朋克风、冷硬派、Show Don't Tell）。
*   **用途**: 提供写作的底层逻辑和风格约束。

### 1.2 动态上下文 (Dynamic Context / Short-term Memory)
*   **存放位置**: `03_Story_Planning/01_Main_Story/`
*   **关键文档**:
    *   `Volume_01_Context_Tracker.md`: **当前状态快照**。记录上一章结束时的：
        *   时间/天气 (Time/Weather)
        *   人物位置与状态 (Location & Status)
        *   持有物品 (Inventory) - *关键，防止道具消失*
        *   未解伏笔 (Open Loops)
    *   `Story_State_Snapshot.md`: 宏观剧情状态（各势力动态）。
*   **用途**: 确保章节之间的连续性，防止逻辑断层。

### 1.3 执行蓝图 (Execution Blueprint / Plan)
*   **存放位置**: `03_Story_Planning/01_Main_Story/`
*   **关键文档**:
    *   `Main_Story_Vol01.md`: **总大纲**。定义了章节结构、核心事件和预期字数。
    *   `Chapter_XXX/Outline.md`: **分章细纲**。在写作前生成的具体场景规划。
*   **用途**: 导航写作方向，确保不偏离主线。

---

## 2. 标准创作流程 (Standard Operating Procedure)

整个创作过程分为五个阶段，形成一个闭环。

### 阶段一：需求分析与规划 (Initiation & Planning)
1.  **用户指令解析**: 识别用户意图（是写新章、改旧章、还是补设定？）。
2.  **上下文加载**:
    *   读取 `Context_Tracker.md` 确认起点。
    *   读取 `Main_Story_Vol01.md` 确认终点。
3.  **冲突检测**:
    *   检查时间线是否连贯？
    *   人物动机是否符合 `Char_*.md`？
    *   *如有冲突，优先修正大纲或设定，绝不强行写作。*

### 阶段二：细纲构建 (Outlining)
*   **操作**: 在 `04_Writing_Workspace/Volume_01_Drafts/Chapter_XXX/` 下创建 `Outline.md`。
*   **内容**:
    *   **本章目标**: 核心冲突是什么？
    *   **场景流**: Scene 1 -> Scene 2 -> Scene 3。
    *   **关键台词/伏笔**: 必须包含的要素。

### 阶段三：正文撰写 (Drafting)
*   **操作**: 创建 `Draft_AI.md`。
*   **策略**:
    *   调用 `Style_Guide` 确保风格统一。
    *   使用沉浸式视角（POV）。
    *   严格遵守物理规则（World Rules）。

### 阶段四：反馈与迭代 (Refinement)
*   **操作**: 用户反馈 -> 修改 -> 生成 `Final_User.md`。
*   **工具**: 使用 `SearchReplace` 进行精准修缮，而非全篇重写（除非结构性崩坏）。

### 阶段五：状态同步 (State Synchronization) - **至关重要**
*   **操作**: 章节定稿后，必须立即更新以下文档：
    1.  **更新 `Context_Tracker.md`**: 推进时间，更新位置，增减道具。
    2.  **更新 `Char_*.md`**: 如果发生了重大性格转变或获得了新能力。
    3.  **更新 `Main_Story_Vol01.md`**: 标记进度，根据实际写法微调后续大纲。

---

## 3. 关键提示词策略 (Key Prompting Strategies)

在与 AI 协作时，系统隐式或显式地使用了以下提示策略：

### 3.1 角色扮演与思维链 (Roleplay & CoT)
*   *"You are a senior pair-programmer and novel editor."*
*   *"Think step-by-step: Analyze the user request -> Check context -> Plan changes -> Execute."*

### 3.2 检索增强生成 (RAG - Manual)
*   *"Before writing, READ the following files: [List of files]."*
*   此策略通过强制读取文件，模拟了 RAG 的检索过程，确保 AI 拥有最新记忆。

### 3.3 约束注入 (Constraint Injection)
*   *"Do not violate the rules in World_Rules_Physics.md."*
*   *"Always check absolute paths."*

### 3.4 状态一致性检查 (State Consistency Check)
*   *"Review Chapter N-1's ending. Does Chapter N start at the correct time and place?"*

---

## 4. 常见工作流示例 (Workflow Examples)

### 场景 A：创作新章节
`Read Outline` -> `Read Context` -> `Write Draft` -> `User Review` -> `Update Context`

### 场景 B：修改设定（吃书）
`Update World_Rules` -> `Search & Replace in Previous Chapters` -> `Update Context` -> `Update Character Cards`

### 场景 C：剧情逻辑修复
`Identify Conflict` -> `Trace Back to Source (Draft or Outline)` -> `Fix Root Cause` -> `Propagate Changes Forward`
