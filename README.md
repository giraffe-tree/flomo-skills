# flomo-skills

把 flomo 和本地连起来的工具集，零基础也能用。

## 已支持的能力

| 能力 | 作用 |
|------|------|
| **flomo-sync** | 支持把 flomo 里的所有笔记备份到电脑，变成 Markdown 文件，支持同步某个时间点后的数据, 支持增量同步和附件下载 |
| **flomo-add** | 往 flomo 里快速新增一条 memo |

更多能力会陆续加入。

## 第一次使用（配置一次，两个能力共用）

 **写 flomo 配置**  

**flomo-sync** 把笔记备份到本地，**flomo-add** 从本地往 flomo 发一条；配置一次，两个都能用，后续还会加更多能力。

在项目根目录创建 `.flomo.config`，按各技能 SKILL.md 中的格式说明填好 `url`（flomo-add 用）与 `token`（flomo-sync 用）。格式为 `key=value` 一行一个，`#` 开头为注释。

## 怎么用

### 1. 安装到 Code Agent

把本仓库中的 skill 接入你的 Cursor（或其它支持 Agent Skills 的 code agent），让 AI 在对话里能自动调用：

| Skill       | 接入后 AI 能做的事 |
|------------|--------------------|
| **flomo-sync** | 备份 flomo、把 memo 同步到本地 Markdown、导出笔记（含增量同步、附件下载） |
| **flomo-add**  | 往 flomo 里快速新增一条 memo、记临时想法、自动化写入单条笔记 |

具体接入方式请按你使用的 agent 文档操作（如 Cursor：在设置中添加/引用本仓库下的 `skills/flomo-sync`、`skills/flomo-add` 等）。

### 2. 日常使用

- **备份 / 同步 flomo**：在对话里说「帮我把 flomo 备份到本地」「同步 flomo 到当前目录」等，会走 flomo-sync。
- **往 flomo 发一条**：说「把这句话记到 flomo：xxx」「往 flomo 加一条：今天学到了…」等，会走 flomo-add。

更细的参数和说明见各 skill 目录下的 `SKILL.md`。

## 常见问题

- **登录失败 / sign 错误**：多半是 token 过期，重新复制一次填进 `.flomo.config`
- **想换备份目录**：改 `--dir` 后面的路径（必须写绝对路径）
- **不想下载附件**：sync 时加 `--no-download`

---

