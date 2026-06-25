---
name: commit-alvin
description: 按固定中文格式提交并推送 git 改动。当用户要求 commit、提交代码、commit and push、保存当前更改到 git 时使用。
---

# commit-alvin

## 工作流

1. 提交前先读取改动范围：`git status`、`git diff`、`git diff --staged`，并看几条近期 `git log` 以对齐历史风格。
2. 把需要提交的文件加入暂存区。不要主动加入疑似密钥或环境文件（`.env`、credential、token 等），如果这类文件已被改动，先提醒用户。
3. 按下面的格式写 commit message，标题日期用当天日期。
4. 提交成功后推送：已有上游分支用 `git push`，首次推送用 `git push -u origin HEAD`。
5. 不做 force push、不跳过 hook、不改 git config。push 失败时只报告原因和下一步，不擅自重试破坏性命令。

## Commit 格式

标题固定为 `YYYYMMDD 类型：一句话说明`，默认类型是 `新增`，根据改动性质可换成 `修复`、`更新`、`重构`、`文档`、`测试`。

正文写清楚四件事：目的、具体更改、已做的验证、后续别人该怎么验证（在什么环境跑什么命令）。

## 模板

```text
YYYYMMDD 新增：一句话说明

目的：说明为什么做这个改动。

更改：稍微详细说明关键代码、配置或行为变化。1、xxx 2、xxx 3、xxx 4、xxx

验证：列出已经跑过的命令和结果。

后续验证：说明其他人应在什么环境下运行什么命令继续验证。
```

## 示例

```text
20260625 新增：MCP 动作冒烟测试脚本

目的：在提交前快速确认动作 MCP 通路可用，避免回归。

更改：1、新增 smoke_test_actions_mcp.py 跑通连接与基础调用 2、补充超时与失败时的清晰报错 3、在 TOOLS.md 登记该脚本用途。

验证：本地 python scripts/smoke_test_actions_mcp.py 通过，退出码 0。

后续验证：在装好依赖的环境里 cd 到仓库根目录运行 python scripts/smoke_test_actions_mcp.py，看到全部用例 OK 即可。
```

## 提交信息写法

用 HEREDOC 传多行 message，保证换行正确：

```bash
git commit -m "$(cat <<'EOF'
20260625 新增：一句话说明

目的：...

更改：1、... 2、... 3、...

验证：...

后续验证：...
EOF
)"
```
