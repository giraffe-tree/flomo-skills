# flomo-skills

把 flomo 和本地连起来的工具集，零基础也能用。

## Skills（技能）

| Skill | 作用 |
|-------|------|
| **flomo-sync** | 将 flomo 笔记备份到本地为 Markdown，支持按时间点同步、增量同步与附件下载 |
| **flomo-add** | 往 flomo 快速新增一条 memo |

更多 skill 会陆续加入。

## 提示词规则（Rules）

| 规则文件 | 作用 |
|----------|------|
| **rules/flomo-nodes.mdc** | 约定笔记库路径、单条 memo 结构，以及查找 / 总结 / 发散 / 写作时的使用方式，供 AI 在项目内正确使用已同步的 flomo 笔记（需在 Cursor 等 agent 中作为规则启用，与 Skills 是不同机制） |

## 第一次使用（配置一次，多能力共用）

在项目根目录创建 `.flomo.config`，按各技能 SKILL.md 的格式填好 `url`（flomo-add 用）与 `token`（flomo-sync 用）。格式为 `key=value` 一行一个，`#` 开头为注释。配置一次，flomo-sync、flomo-add 及后续能力均可复用。

## 怎么用

### 1. 安装 Skills

将本仓库的 skill 接入 Cursor（或其它支持 Agent Skills 的 code agent），AI 在对话中即可自动调用：

| Skill | 接入后 AI 能做的事 |
|-------|--------------------|
| **flomo-sync** | 备份 flomo、同步 memo 到本地 Markdown、导出笔记（含增量、附件） |
| **flomo-add** | 往 flomo 快速新增一条 memo、记临时想法、自动化写入单条笔记 |

接入方式：在 agent 设置中引用本仓库下的 `skills/flomo-sync`、`skills/flomo-add`。

### 2. 启用规则（可选）

若希望 AI 在项目内基于已同步笔记做查找、总结、发散或写作，需单独启用**规则**（与 Skills 不是同一类配置）。在 Cursor 中将 `rules/flomo-nodes.mdc` 作为规则添加后，AI 会按其中约定使用 `output/flomo-sync/` 的笔记库位置与结构，并正确引用与回溯来源。

### 3. 日常使用

- **备份 / 同步 flomo**：在对话里说「帮我把 flomo 备份到本地」「同步 flomo 到当前目录」等，会走 flomo-sync。
- **往 flomo 发一条**：说「把这句话记到 flomo：xxx」「往 flomo 加一条：今天学到了…」等，会走 flomo-add。
- **基于笔记查找 / 总结 / 写作**：启用规则 `rules/flomo-nodes.mdc` 后，AI 会按规则在 `output/flomo-sync/` 内检索、归纳或延伸，并保留来源可追溯。

更细的参数与说明见各 skill 目录下的 `SKILL.md`。

## 常见问题

- **登录失败 / sign 错误**：多半是 token 过期，重新复制一次填进 `.flomo.config`
- **想换备份目录**：改 `--dir` 后面的路径（必须写绝对路径）
- **不想下载附件**：sync 时加 `--no-download`

---

