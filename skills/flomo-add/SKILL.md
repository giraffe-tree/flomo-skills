---
name: flomo-add
description: 通过 Python requests 向 flomo webhook URL 新增一条 memo。使用 scripts/flomo-add.py 从 .flomo.config 读取 url 并发起 POST 请求，支持在 macOS 与 Windows 环境下添加 flomo 笔记。用户需要快速新增 flomo 记录、写入临时想法、或自动化写入单条 memo 时使用。
---

# flomo-add

向 flomo 新增一条 memo（单条写入）。

## 前置入参要求（必须）

执行本技能前，必须先明确并拿到以下入参：

- 当前项目主路径（绝对路径），例如 `/Users/xxx/project-name`
- memo 文本内容（即本次要写入 flomo 的 `content`）

必须在“当前项目主路径”下存在 `.flomo.config`，并且包含 `url=<flomo webhook url>`。

## 配置（必须）

```bash
cp assets/.flomo.config.example /Users/xxx/project-name/.flomo.config
# 编辑 .flomo.config，填入 url=https://flomoapp.com/iwh/...
```

`.flomo.config` 使用 `key=value` 格式，`#` 开头行表示注释，与 `flomo-sync` 一致。

## 快速开始

### 1) 使用 Python 脚本（推荐，内部调用 requests）

```bash
# 在项目主路径下执行
python skills/flomo-add/scripts/flomo-add.py --content "Hello, #flomo https://flomoapp.com"
```

可选参数：

- `--config`：指定配置文件路径（默认 `.flomo.config`）
- `--url`：临时覆盖配置里的 `url`
- `--dry-run`：只打印将发送的请求信息，不真正发送

### 2) 直接使用 curl（macOS / Linux）

```bash
curl -X POST "https://flomoapp.com/iwh/M000000/abcdefg0000000000000000000000000/" \
  -H "Content-Type: application/json" \
  --data-binary '{"content":"Hello, #flomo https://flomoapp.com"}'
```

### 3) 直接使用 curl（Windows PowerShell）

```powershell
$url = "https://flomoapp.com/iwh/M000000/abcdefg0000000000000000000000000/"
$body = '{"content":"Hello, #flomo https://flomoapp.com"}'
curl.exe -X POST $url -H "Content-Type: application/json" --data-binary $body
```

## 预期行为

- 成功时：返回 flomo API 响应并退出码为 0
- 失败时：脚本打印错误原因（缺少配置、requests 依赖缺失、HTTP 失败等）并退出非 0

## 文件说明

```text
skills/flomo-add/
├── SKILL.md
├── scripts/
│   └── flomo-add.py
└── assets/
    └── .flomo.config.example
```
