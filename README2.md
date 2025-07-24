# 启元大赛团队协作指南说明书

欢迎加入我们的小队！为了让我们在比赛中高效协作、避免混乱、共同进步，我们约定以下协作流程和工具使用方法。请仔细阅读并严格遵守。

## 1. 核心准则：Git 与 GitHub 工作流 (`Feature Branch Workflow`)

这是我们代码协作的生命线，**所有代码的修改都必须遵循此流程**。

### 核心原则
*   **`main` 分支是神圣的**：任何人**禁止**直接向 `main` 分支推送 (`push`) 代码。`main` 分支只接受通过 Pull Request 合并的代码，以确保其随时都是稳定可运行的。
*   **先同步，再开发**：每次开始新任务前，请先从上游（`upstream`）仓库拉取最新的 `main` 分支，确保自己的代码库是最新版本。
    ```bash
    # 切换到 main 分支
    git checkout main

    # 从原始比赛仓库（我们称之为 upstream）拉取最新代码
    git fetch upstream
    
    # 合并 upstream/main 到你本地的 main
    git merge upstream/main
    
    # 推送最新的 main 到我们自己 fork 的仓库（我们称之为 origin）
    git push origin main
    ```

### 开发流程

1.  **为每个任务创建新分支**：无论是开发一个新算子还是修复一个Bug，都要从最新的 `main` 分支创建新的 `feature` 分支。分支命名要清晰，格式为 `类型/简短描述`。
    ```bash
    # 确保你从最新的 main 分支开始
    git checkout main 
    
    # 创建并切换到新分支（例如，开发 LeakyReLU 算子）
    git checkout -b feature/leaky-relu
    ```

2.  **在你的分支上编码**：在你的新分支上自由地进行开发和调试。无论是以姓名命名的个人分支,还是以内容命名的功能分支,注意都保证在分支上进行开发测试.

3.  **频繁、清晰地提交**：完成一个小的、有意义的功能点后，就进行一次提交 (`commit`)。Commit Message 要写得清晰明了。
    ```bash
    # 添加所有修改
    git add .

    # 编写一个清晰的 commit message
    git commit -m "feat: 实现 LeakyReLU 的前向计算"
    # 或 "fix: 修复 LeakyReLU 在负数输入时的计算错误"
    ```

4.  **推送到远程分支**：将你的本地分支推送到我们 Fork 的远程仓库 (`origin`)。
    ```bash
    git push origin feature/leaky-relu
    ```

5.  **代码审查 (Code Review) 与合并**：
    *   队友会审查你的代码，提出修改意见。
    *   你根据意见进行修改，并再次 `push` 到你的分支（PR会自动更新）。
    *   直到所有人都同意后，这个 PR 才会由我们共同决定合并（或根据比赛规则提交）。

6.  **创建 Pull Request (PR)**：在 GitHub 上，从你的 `feature/leaky-relu` 分支向原始比赛仓库的 `main` 分支发起一个 Pull Request。
    *   **标题**：清晰地写明这个 PR 的目的，比如 `[T1-1-1] Add LeakyReLU Operator`。
    *   **描述**：详细说明你做了什么、实现了哪些功能、如何测试的。**这是评审的关键依据！**
    *   **Reviewers**: 在右侧的 `Reviewers` 栏中，选择你的队友，`@` 他来进行代码审查。


## 2. 终端和交流工具：Tmux和Live Share

当我们遇到难题，需要像坐在一起一样共同调试时，请使用以下工具：

### VS Code Live Share (强烈推荐)
这是最高效的远程协作方式。
*   **功能**: 实时共享代码编辑、共享终端、共享调试会话。
*   **用法**: 一位同学在 VS Code 中通过 `Remote-SSH` 连接到服务器并打开项目，然后点击左下角的 `Live Share` 按钮生成并分享链接。另一位同学点击链接即可加入。

### `tmux` 终端共享
建议的方式是每一个人创建一个自己姓名的Tmux终端,在这个终端中进行命令操作.
常用的命令:
- 创建终端:tmux new -s <名称>
- 载入终端:tmux a -t <名称>
- 暂时离开终端 ctrl+B D

如果只想快速共享一个终端界面。
*   **功能**: 两人看到完全一样的终端屏幕，并可以同时操作。
*   **用法**:
    ```bash
    # 同学A 创建会话
    tmux new -s pair-debug

    # 同学B 加入会话
    tmux attach -t pair-debug
    ```

## 3. 方案设计与文档协作:飞书文档

好的文档是成功的一半，也是比赛的最终产出之一。

**工具：飞书文档**

*   **技术方案设计**: 在动手写复杂代码前，先共同在文档中把设计思路、模块划分、API 接口等讨论清楚。这份文档也是我们 PR 描述和最终技术报告的基础。
*   **会议纪要**: 每次讨论后，用几分钟记录下关键结论和任务分配 (TODO List)。
*   **知识库**: 记录遇到的重要问题、解决方案、环境配置的详细步骤等，避免重复踩坑。

## 4. 任务同步：沟通与任务管理

确保我们总是在为同一个目标努力，并且信息通畅。

### 日常沟通：飞书 / 微信
用于快速提问、临时讨论等非正式沟通。

### 正式任务管理：GitHub Issues
*   **创建任务**: 将每一个待开发的功能或待修复的 Bug，在 **我们 Fork 的仓库** 里创建一个 Issue。
*   **分配任务**: 在 Issue 中使用 `@` 功能，明确指派给负责人。
*   **关联进度**: 在我们的 Commit Message 或 PR 中，可以通过 `#Issue编号` (例如 `#12`) 来关联对应的 Issue，方便追踪任务的完成情况。

---

### 工作流示例 

1.  **工作记录**: 在**飞书**上快速同步：昨天做了什么？今天计划做什么？遇到了什么问题？
2.  **领取任务**: 从 **GitHub Issues** 中发布或领取一个任务（比如 "Issue #5: 实现 Exp 算子"）。(可以不用)
3.  **开始编码**:
    * 先切换到自己的分支和tmux中 `tmux a -t <姓名>` `git checkout <分支名>`
    *   `git checkout main`, `git fetch upstream`, `git merge upstream/main` (同步最新代码)。
    *   `git checkout -b feature/exp-operator-#5` (创建新分支，并关联 Issue)。
4.  **合作解决问题**: 开发中遇到困难，通过 **VS Code Live Share** 邀请队友一起结对调试。
6.  **Code Review**: 看到队友的 PR 通知后，及时审查代码并给出反馈。
5.  **提交PR**: 功能完成并通过本地测试后，`git push` 并创建 **Pull Request**，在描述中附上**飞书文档**里的设计思路，并 `@` 队友进行 Code Review。
7.  **注意事项**: 确保自己分支的代码已提交，并在 Issue 中更新自己的进度。

---

> 让我们遵循规范，高效协作，享受比赛！祝我们合作愉快，取得好成绩！