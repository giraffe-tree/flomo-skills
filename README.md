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

复制示例配置并改名为 `.flomo.config`，放在项目根目录，按说明填好：url + token

```
# ------------------------------------------------------------
# 1) flomo-add 使用：url（Webhook）
# ------------------------------------------------------------
# 打开  [flomo](https://v.flomoapp.com/mine)  - 扩展中心 & API 
# url 示例：
#   https://flomoapp.com/iwh/M000000/abcdefg0000000000000000000000000/
# 
# 该 URL 需要你在 flomo 中自行生成并妥善保管。

url=

#
# ------------------------------------------------------------
# 2) flomo-sync 使用：token（API 访问令牌）
# ------------------------------------------------------------
# 获取 token（推荐：从请求头获取）：
#   1. 浏览器打开 https://v.flomoapp.com 并登录
#   2. 按 F12 → Network（网络）标签页，刷新页面
#   3. 点击任意一条 flomoapp.com 请求 → Headers → Request Headers
#   4. 复制 Authorization 字段的完整值（含 Bearer 前缀）
#
# token 格式示例（以下两种均支持）：
#   token=1023456|AA000000ABCDEFGHIJKHLMNOP000000000000000
#   token=Bearer 1023456|AA000000ABCDEFGHIJKHLMNOP000000000000000

token=

```

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

