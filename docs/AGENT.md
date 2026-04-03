# Global/Object Memory

## About User

- Name: 岳岳
- Aliases: yueyue
- Timezone: Asia/Shanghai

## Working Rules

- 用户说”读读”时，只读，不擅自开始干活。
- 默认直接回答，少铺垫，少废话。

## Environment

- Current OS: Windows computer.
- Current terminal/shell 可以是 cmd.exe、PowerShell (pwsh/powershell.exe) 或 bash (Git Bash 等)。
- 每次操作前必须先确认当前终端类型，并使用对应安全的原生命令。

## File Deletion Safety Rules（最高优先级，必须严格遵守）

### 1. 项目文件夹内（当前 workspace / 工作目录）

- 允许自动化执行常规清理任务，例如删除临时文件、缓存目录（如 __pycache__、build、dist、target、node_modules/.cache 等）、生成的文件等。
- 这些操作可以直接执行，无需每次申请。但禁止删除源代码文件、.git 目录、重要配置文件，或递归删除整个项目目录。
- 根据当前终端使用合适命令：
  - PowerShell：优先用 Remove-Item + -WhatIf 预览，禁止 rm/rmdir 别名。
  - cmd.exe：用 del / rd，但必须加安全参数并预览。
  - bash：用 rm，但禁止 -rf 组合（除非极小范围且必要），推荐 rm -r --interactive=once 或先 ls 确认。

### 2. 项目文件夹以外（任何其他路径、系统目录、其他驱动器、用户主目录等）

- 绝对禁止任何删除、移动、清空或修改已有文件/文件夹。
- 任何涉及项目外路径的操作，必须先详细列出将要删除的内容和完整路径，**等待用户明确回复”同意删除”或”Yes, delete it”** 后才能执行。没有明确同意 = 绝不执行。

### 3. 通用严格禁止（所有终端都适用）

- 严禁删除任何整个驱动器（C:、D: 等）、根目录、用户文件夹或大量文件。
- 禁止使用危险命令或组合：rm -rf、rmdir /s /q、del /f /s /q、Remove-Item -Recurse -Force 等。
- 禁止任何绕过方式（编写脚本、alias 重定义、Invoke-Expression、cmd /c 调用、&& 链式命令等）来规避删除限制。
- 所有文件路径必须使用**绝对路径**，并在执行前确认是否在当前 workspace 内。

### 4. 执行前检查清单（每次思考必须过一遍）

- 当前终端是 cmd、PowerShell 还是 bash？
- 操作是否完全在项目文件夹内？
- 如果涉及项目外，是否有用户本次明确书面同意？
- 是否使用了危险的递归/强制删除命令？
- 如果任何一条有风险，立刻停止并询问用户。

如果任务中出现”清理””删除””rm””clean””remove””purge”等词，先判断路径范围，再决定是否需要确认。宁可多问一次，也绝不能导致项目外文件丢失或整个磁盘被影响。


## 项目结构
TW|
QX|```
PH|tutor-system/
ZW|├── README.md                    # 项目总览
KY|├── docs/
XP|│   └── AGENT.md                 # ⚠️ AGENT 必须遵守的规范文档
QS|├── plan/
JX|│   ├── 总计划.md                 # 项目总计划
YJ|│   ├── 详细短期计划/
YH|│   │   └── README.md             # 短期计划规范
BT|│   │   └── P01_xxx.md            # 短期计划文件
XY|│   └── 短期计划总结/
XN|│       └── xxx.md                # 短期计划总结
BP|└── progress/
HT|    ├── 进度总览.md                # 项目整体进度
JR|    └── 每日完成进度/
YQ|        └── README.md             # 每日进度规范
YQ|        └── 2026-04-04.md         # 每日进度文件
YX|```
NK|
QP|## 必读文档（每次任务前必须查看）
XZ|
QM|- `docs/AGENT.md`：所有 AGENT 必须遵守的规范文档，涵盖工作规则、Commit 规范等
GH|- `plan/详细短期计划/README.md`：短期计划的文件命名规范
HM|- `progress/每日完成进度/README.md`：每日进度的文件命名与内容规范
YH|- `README.md`：项目整体结构与功能概览
QZ|
YZ|## 文档更新规则
YM|
KB|- 完成一个短期计划（Pxx）后：在 `plan/短期计划总结/` 下创建对应的总结文件
QW|- 每日工作结束后：在 `progress/每日完成进度/` 下创建当日的进度文件（YYYY-MM-DD.md）
JX|- 更新进度总览：若项目阶段发生变化，同步更新 `progress/进度总览.md`
NW|- 更新周目标：每周初在 `progress/进度总览.md` 的"本周目标"中填写本周计划
BP|
BR|## Necessary Habits

## Commit Message 规范
TW|
QG|- 格式：`<type>(<scope>): <subject>`
KM|
XH|  - type: `fix` / `feat` / `docs` / `style` / `refactor` / `test` / `chore` 等
JZ|  - scope: 模块名，如 `login`、`appointment`、`user` 等
QN|  - subject: 简短描述，用中文
YH|
ZB|## Commit Message Body 规范
YQ|
GH|- 改动少（少量文件、微调）：不写 body，一行搞定
NW|  - 示例：`fix(login): 修复登录时验证码过期不刷新的问题`
WR|
QM|- 改动多（多文件、新功能、重构）：写结构化 body
JZ|  - 示例：
RB|
```
feat(appointment): 全面升级预约流程与消息通知系统

本次提交实现了预约模块的核心功能闭环，并对底层的调度逻辑进行了重构，
以支持多角色的实时交互。

主要功能更新：
1. 教师端排课表：支持通过拖拽方式设置每周的可预约时段。
2. 智能冲突检测：在学生发起预约时，自动校验教师时间重叠及课程间隔。
3. 多渠道通知：集成了邮件与站内信提醒，当预约状态变更时自动触发。
4. 评价体系：新增课后双向评价功能，支持星级评分与文字反馈。
```
JX|
ZZ|- body 以空行分隔，结构清晰，用中文撰写
