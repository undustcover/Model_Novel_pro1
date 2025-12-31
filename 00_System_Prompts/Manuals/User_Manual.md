# Trae Novel Assistant - 用户操作手册 (User Manual)

本文档旨在指导用户如何高效地与 Trae AI 协作，维护文档体系，确保长篇小说的逻辑连贯性与创作质量。

## 1. 文档体系导览 (Documentation System)

本系统采用**分层文档结构**，分为全局设定、分卷文档和系统指令。

### 1.1 全局设定 (Global Settings) - `01_World_Bible/` & `02_Characters/`
*   **作用**: 定义整个小说宇宙的物理法则、社会结构、核心人物属性。
*   **性质**: **公理 (Axioms)**。除非发生重大剧情转折（如世界重启），否则不应随意更改。
*   **关键文件**:
    *   `World_Rules_Physics.md`: 异能体系与代价。
    *   `Char_*.md`: 人物核心档案（性格、内驱力）。

### 1.2 分卷文档 (Volume Docs) - `03_Story_Planning/Volume_XX_Docs/`
*   **作用**: 定义特定卷/阶段的创作约束和剧情状态。
*   **性质**: **动态 (Dynamic)**。随着剧情推进而不断更新。
*   **关键文件**:
    *   `Volume_XX_World_Rules.md`: **本卷的特殊限制**（如“反向提示词”）。
    *   `Volume_XX_Worldline_Log.md`: **权限控制**（当前阶段能写什么，不能写什么）。
    *   `Volume_XX_Context_Tracker.md`: **当前状态**（上一章结束时的天气、道具、伏笔）。
    *   `Volume_XX_Outline.md`: 分章大纲。

### 1.3 系统指令 (System Instructions) - `00_System_Prompts/` & `.cursorrules`
*   **作用**: 指导 AI 如何思考、如何写作、如何检查逻辑。
*   **性质**: **元规则 (Meta-Rules)**。
*   **关键文件**:
    *   `.cursorrules`: 根目录下的 AI 行为准则，强制 AI 在写作前读取特定文档。

---

## 2. 创作流程检查清单 (Workflow Checklists)

### 2.1 每次请求生成新章节前 (Pre-Generation)
用户无需手动操作，系统会自动执行（根据 `.cursorrules`），但用户应知晓系统在做什么：
1.  读取 `Volume_XX_Context_Tracker.md` -> 获取上下文。
2.  读取 `Volume_XX_Worldline_Log.md` -> 确认当前权限。
3.  读取 `Volume_XX_World_Rules.md` -> 加载反向提示词。

### 2.2 每次章节完成后 (Post-Generation)
**[重要]** 用户定稿（保存 `Final_User.md`）后，系统需要执行以下更新。如果系统忘记了，请提示：“更新文档状态”。
1.  **更新 `Volume_XX_Context_Tracker.md`**:
    *   更新时间、地点、天气。
    *   更新人物持有物品、身体状态。
    *   记录新挖的坑（伏笔）。
2.  **更新 `Volume_XX_Worldline_Log.md`**:
    *   如果剧情进入了新阶段（如从“日常篇”进入“危机篇”），解锁相应的写作权限。

### 2.3 每卷完结后 (Post-Volume)
1.  **归档**: 将本卷的 `Context_Tracker` 归档为历史记录。
2.  **升维**:
    *   检查是否有分卷设定变成了全局设定？（如主角获得了永久性能力，需写入 `02_Characters`）。
    *   检查世界观是否有永久性改变？（需更新 `01_World_Bible`）。
3.  **创建新卷**:
    *   建立 `Volume_02_Docs` 文件夹。
    *   复制并重置 `World_Rules` 和 `Context_Tracker`。

---

## 3. 变更管理指南 (Change Management)

当用户想要修改设定时，请遵循以下路径：

### 3.1 修改人物设定 (Character Change)
*   **场景**: 用户想让苏浅从“高冷”变成“逗比”。
*   **操作**:
    1.  修改 `02_Characters/Protagonist/Char_Heroine_SuQian.md`。
    2.  **[关键]** 检查 `Volume_XX_World_Rules.md` 中的“反向提示词”，确保没有冲突（如“禁止破壁”是否限制了逗比属性？）。

### 3.2 修改世界观/吃书 (Retcon)
*   **场景**: 用户决定泰坦科技其实不是垄断者，而是傀儡。
*   **操作**:
    1.  修改 `01_World_Bible/Factions_Matrix.md`。
    2.  在 `Volume_XX_Worldline_Log.md` 的“历史变动记录”中记一笔，防止 AI 混淆旧设定。

### 3.3 调整创作原则 (Principle Adjustment)
*   **场景**: 用户觉得现在的文风太压抑，想要更轻松一点。
*   **操作**:
    1.  修改 `00_System_Prompts/Style_Guide.md`。
    2.  或者在 `Volume_XX_World_Rules.md` 中添加新的指导原则。

---

## 4. 如何优化系统 (System Optimization)

为了让系统更懂你：
1.  **多用反向提示词**: 在 `Volume_XX_World_Rules.md` 的第 0 章中，明确列出**“我不喜欢的写法”**。这是最直接有效的调教方式。
2.  **维护上下文**: `Context_Tracker` 越准确，AI 写的下一章就越连贯。不要让它猜上一章发生了什么。
3.  **阶段性复盘**: 每隔几章，回顾一下 `Worldline_Log`，确认剧情是否还在预设的轨道上。

---

**核心口诀**:
*   改设定 -> 动 `01`/`02`
*   改剧情 -> 动 `03`
*   改文风 -> 动 `00`
*   写新章 -> 读 `Context` + `Rules`
