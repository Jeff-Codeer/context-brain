# 操作日志

只追加，不改已经写下的条目。

## 2026-10-23 · 迁入 LLM Wiki，停用 kb-e5dcbd5b

- 把原 `kb-e5dcbd5b/meetings/` 三份纪要按原文字复制到 `raw/meetings/`，并在 `wiki/meetings/` 加上编号和链接。横线以下与 raw 一致。
- 新建编译页：`wiki/topics/企业AI转型.md`、`wiki/topics/车型可诊断性.md`、`wiki/topics/业务出海.md`、`wiki/people/易博.md`、`wiki/people/友明.md`、`wiki/people/倪天宇.md`。
- 公开入口改为 `wiki/index.md`：https://jeff-codeer.github.io/context-brain/wiki/index.md
- 删除 `kb-e5dcbd5b/`（含 `index.md`、`index.html`、`meetings/`）。该路径不再提供内容，也不再做同步副本。
- 会议编号沿用迁移前的目录：M1 企业 AI 转型，M2 车型可诊断性，M3 业务规划。没有新的飞书妙记。
- 待办保持源纪要的未勾选。源纪要中的「次日」按会议日 2026-10-22 换算为 2026-10-23；本次迁移没有材料证明这些事项已完成，因此在目录里标为未完成，时间点已到的标为待核对（见 AGENTS.md 巡检），不改为完成。
- 措辞未合并：M3 总结写「烧车、冒烟为可管控的核心安全事件；撞击导致的人员伤亡暂不属于可干预技术覆盖范围」；智能章节 [06:39] 写「烧车、冒烟、死人是三类底线问题」，并写撞击致底盘刺穿引发的电池内部燃烧无法靠控制器干预。两套句子都保留在 [业务出海](topics/业务出海.md#安全事件清单)。章节标题原文是「超车清单中相关风险点及可解决问题」，总结用的是「安全事件清单」，未把这两个称呼收成同一个专名。
