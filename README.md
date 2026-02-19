# flomo-skills

把 flomo 和本地连起来的工具集，零基础也能用。

## 已支持的能力

| 能力 | 作用 |
|------|------|
| **flomo-sync** | 支持把 flomo 里的所有笔记备份到电脑，变成 Markdown 文件，支持增量同步和附件下载 |
| **flomo-add** | 往 flomo 里快速新增一条 memo |

更多能力会陆续加入。

## 第一次使用（配置一次，两个能力共用）

 **写 flomo 配置**  

   复制示例配置并改名为 `.flomo.config`，放在项目根目录，按说明填好：url + token

```
# ------------------------------------------------------------
# 1) flomo-add 使用：url（Webhook）
# ------------------------------------------------------------
# webhook url 示例：
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

安装到你的 code agent 中即可

name: flomo-sync
description: 将 flomo 所有记录 memo 同步/备份到本地 Markdown 文件的工具。使用 scripts/flomo-sync.py 脚本通过 flomo API 拉取 memo，支持增量同步、附件下载、多文件输出。当用户需要备份 flomo、同步 flomo memo 到本地、导出 flomo 笔记为 Markdown 时使用。

name: flomo-add
description: 通过 Python requests 向 flomo webhook URL 新增一条 memo。使用 scripts/flomo-add.py 从 .flomo.config 读取 url 并发起 POST 请求，支持在 macOS 与 Windows 环境下添加 flomo 笔记。用户需要快速新增 flomo 记录、写入临时想法、或自动化写入单条 memo 时使用。

详细参数和说明见各 skill 目录下的 `SKILL.md`。

## 常见问题

- **登录失败 / sign 错误**：多半是 token 过期，重新复制一次填进 `.flomo.config`
- **想换备份目录**：改 `--dir` 后面的路径（必须写绝对路径）
- **不想下载附件**：sync 时加 `--no-download`

---

一句话：**flomo-sync** 把笔记备份到本地，**flomo-add** 从本地往 flomo 发一条；配置一次，两个都能用，后续还会加更多能力。
