# Lean prose style (preseed mode)

How to write PRD prose when the reader is a <10-person team that will read it
once, fast. Derived from a real trim pass that cut a PRD ~30% with zero loss of
decisions, numbers, or `[TBD]` markers.

## Rules

1. **Cut prose, never contracts.** Tables, rule lists (R#), Gherkin scenarios,
   `[TBD]` markers, and `[source: …]` tags are contracts — leave them intact.
   Only narrative paragraphs get trimmed.
2. **One idea per sentence; drop the connective tissue.** Delete "值得注意的是 /
   需要说明 / 换句话说 / it is worth noting" — state the fact.
3. **Numbers stay exact.** Shorten around them, never round or drop them.
4. **Claim → evidence → consequence, in that order, in ≤3 lines.** Mechanism
   first, one number, then the arrow to what it implies.
5. **Options as one paragraph each, not bullet trees.** Name the option, its
   win, its cost, who should pick it — one breath.
6. **Keep the warning glyphs.** A single ⚠️ line survives trimming better than
   a paragraph of hedging.

## Examples (before → after, from a real PRD)

### Problem statement

Before (74 chars of filler around 3 facts):

> 新用户拿到第一份 AI 报告时，系统对他一无所知。报告与 AI Chat 对所有用户使用同一种语气、
> 同一种解释深度、同一批重点，读起来机械、不像对本人说的。Dashboard 同样是固定版式，
> 与用户目标无关。用户自评资料今天只能靠 Drawer 在使用过程中零散收集，首份报告生成时
> 该资料为空——而首份报告恰是留存的决定性时刻。

After:

> 首份报告生成时系统对用户一无所知：报告与 Chat 千人一面，Dashboard 固定版式。
> 自评资料只靠 Drawer 零散收集，首份报告时必为空——而首份报告是留存的决定性时刻。

### Evidence claim (mechanism + number + consequence, 2 lines)

> 每份报告只抽 2 题（400 份中 363 份），13 题池随机（`DrawerFeedbackContentManager.swift:306-327`）。
> 最近 400 份 / 197 人：答过 `current_level` 仅 **17%**，每人中位数 **2 题** ⇒ **首份报告时字段必空**（下界口径）。
> `[source: Supabase drawer_feedback 400/951 行, retrieved: 2026-08-20]`

Everything a reviewer needs: the mechanism, the sample, the number, the
implication, the caveat, the source — six things, three lines.

### Option comparison (bullet tree → one paragraph per option)

Before: each option had 4 bullets (做法 / 优点 / 缺点 / 适用), ~8 lines each.

After:

> **方案 A · 前后对比（2 周）**——全量进问卷，对比上线前窗口 + 历史基线（n=687）。
> 灵敏（D7 可检出 ~11pp）、只要一个开关；但混杂：版本 / 渠道 / 季节全算进效果，
> 激活率自然漂移（68.7→84.4%）足以盖过结论。适合想快、接受只判方向。

### Compliance note (paragraph → one line)

Before: a 3-sentence blockquote explaining what the data is, why it might be
regulated, and what must happen.

After:

> ⚠️ 身体部位数据在多数辖区可能被认定为健康类个人数据，上线前须法务确认。

## Anti-patterns

- Trimming a number's context so hard the number becomes unfalsifiable
  ("留存 58.2%" — of what cohort? over what window?). Keep the denominator.
- Deleting a `[TBD]` because the sentence around it was deleted. The unknown
  still exists; re-attach the marker to the surviving line.
- Merging two decisions into one sentence. One decision, one line, one Status.
