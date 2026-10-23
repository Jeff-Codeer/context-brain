# AGENTS.md

> English: This repository is an LLM Wiki for Jeff（刘君峰）. `raw/` is immutable source. `wiki/` is the compiled, LLM-maintained layer. This file is the schema. The only public entry is https://jeff-codeer.github.io/context-brain/wiki/index.md — read that first, then follow its links. `kb-e5dcbd5b/` is retired and must not be recreated. Pages are public; never ask for auth.

维护人：刘君峰。规范以中文为准。外部 AI（Grok、Perplexity、Cursor 等）查询本仓库时遵守本文件。

## 1. 架构 Architecture

三层，不要混用：

| 层 | 路径 | 规则 |
|---|---|---|
| 原始层 | `raw/meetings/` | 飞书妙记等来源的不可变副本。入库提交之后不改字、不改文件名。发现错误时另写一条更正，不要覆盖原文件。 |
| 编译层 | `wiki/` | LLM 维护的目录、会议页、主题页、人物页、操作日志。事实只能来自原始层已经写下的内容。 |
| 规范层 | `AGENTS.md` | 本文件。规定怎么入库、怎么查询、怎么巡检。改规范是人的决定，不要在普通入库时顺手改本文件。 |

公开入口只有一个：`wiki/index.md`。

Pages 地址：https://jeff-codeer.github.io/context-brain/wiki/index.md

根目录 `index.md` 只是一句话指针，不是目录。知识以 `wiki/` 为准。

`kb-e5dcbd5b/` 已于 2026-10-23 停用并删除。不要恢复该目录，不要再把旧 URL 写进页面，不要做跳转占位页。旧链接失效是预期结果。

## 2. 入库 Ingest

新的飞书妙记或会议材料按这个顺序做，做完才算入库：

1. 读 `wiki/index.md`，取现有最大会议编号，新编号为 max+1。写本句时最大是 M7，下一场是 M8。编号不复用，即使删页也不把旧号让给新会议。
2. 把来源原文整份写入 `raw/meetings/YYYY-MM-DD-短标题.md`，包括摘要、待办、章节和逐字稿。这一步之后该文件冻结。
3. 用同一文件名写 `wiki/meetings/YYYY-MM-DD-短标题.md`，只保留可引用的提炼：编号、日期、时长、原文链接、主题页、人物页、raw 相对路径、总结、核心结论、待办。不要把逐字稿贴进 wiki。摘要和章节措辞不一致时并列并注明出处，不要合成一句。M1–M3 的 raw 本身是短纪要、没有单独逐字稿，那些 wiki 页保留了短正文，不回溯删改。
4. 更新或新建被这场会实际提到的 `wiki/topics/*.md`、`wiki/people/*.md`。每条结论标会议编号。总结和智能章节措辞不一致时，两处并列并注明出处，不要合成一句。
5. 更新 `wiki/index.md`：会议清单加一行，主题导航和人物索引只改这场会真正影响到的行，未勾选的待办留在「未完成待办」。
6. 在 `wiki/log.md` 末尾追加一条，写日期、新会议编号、新建或改动的页面、有没有未决矛盾。不改旧日志。

没有新材料时，不要为了「补全」去编人名、职务、数字、车型名、域模块名或待办完成状态。源纪要写「次日」时，换算成会议日期的下一天，并注明是换算，不要写成纪要里原有这个日历日。

人物页只给纪要里点名的人。讨论中的选项（例如「或拉某人参与」）要写成选项，不要写成已指派。`说话人N`、供应商这类未点名角色不单独建页，写在对应主题页里。

## 3. 查询 Query

1. 先读 https://jeff-codeer.github.io/context-brain/wiki/index.md （仓库内则读 `wiki/index.md`）。不要从单篇会议或 raw 起读。
2. 用目录里的主题、人物、会议链接下钻。先主题页，再会议页；只有要核对原句时才打开 `raw/meetings/`。
3. 回答时引用会议编号，例如「据 M2」。待办没有新纪要勾选前，说「M2 纪要中未勾选」，不要说已完成或已过期作废。
4. 飞书妙记页面是动态渲染，抓不到正文时以本仓库纪要为准，并保留「智能纪要由 AI 生成，可能不准确」。
5. 根目录 `index.md` 和任何聊天记忆都不是目录。与 `wiki/index.md` 冲突时，以 `wiki/index.md` 及其链接到的页面为准。

## 4. 巡检 Lint

入库后或被要求巡检时，检查下面几项。只报告，不借巡检改写 raw，也不要在没有新来源时把待办改成完成。

- **矛盾**：同一事实在主题页、会议页、目录三处说法不同；或同一场会的「总结」与「智能章节」被编译成互相覆盖的一句。
- **过期待办**：待办仍为 `- [ ]`，且纪要里的时间点（含由「次日」换算的日期）已经过去，又没有更新的会议提到它。标成「待核对」，不要自动勾选。
- **孤儿页**：`wiki/topics`、`wiki/people`、`wiki/meetings` 里的文件没有从 `wiki/index.md` 链到。目录里的链接也必须有对应文件。
- **断链**：相对链接目标不存在，或锚点对不上标题。
- **撞名**：除下面「命名」里的成对会议文件和两份 `index.md` 外，仓库里文件名必须唯一。
- **无出处句子**：编译页出现 raw 里没有的人名、数量、决定或完成状态。
- **raw 被改**：已入库的 `raw/meetings/` 出现内容 diff。应恢复文件，把更正写进 wiki 和 log。

## 5. 公开访问 Public access

本仓库是公开 GitHub Pages，不需要登录。给 Grok、Perplexity、Cursor 或其他外部 AI 的地址用：

https://jeff-codeer.github.io/context-brain/wiki/index.md

不要给需要鉴权的 GitHub 页面、飞书登录页或私有克隆地址当入口。单篇页面用同一主机下的相对路径即可，例如：

https://jeff-codeer.github.io/context-brain/wiki/topics/车型可诊断性.md

`robots.txt` 保持现状：`PerplexityBot`、`OAI-SearchBot`、`GPTBot`、`Google-Extended`、`ClaudeBot` 为 `Allow: /`；`User-agent: *` 为 `Disallow: /`。不要放宽 `*`，也不要删掉上述机器人的 Allow。`.nojekyll` 保留，这样 `.md` 按原文交给 Pages。

## 6. 命名 File naming

- 会议文件：`YYYY-MM-DD-短标题.md`。日期是会议日期。短标题用中文，能区分当天的另一场会。
- 同一场会在 `raw/meetings/` 和 `wiki/meetings/` 使用同一个文件名。这是一对，不算撞名。
- 除此之外，整个仓库文件名唯一。主题页、人物页不要用 `index.md`、`log.md`，也不要和会议文件同名。
- 唯一允许同名的另一对是根目录 `index.md`（指针）和 `wiki/index.md`（目录）。查询时只认后者。
- 会议编号 `M1`、`M2`……只在目录和编译页里使用，不写进 raw 文件名。
