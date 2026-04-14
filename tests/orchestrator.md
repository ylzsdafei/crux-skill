# Test Orchestrator（测试执行流程）

每次 Model/SKILL/protocols/guards 改动后必跑。

## 触发条件

- `models/*.md` 内容变更
- `SKILL.md` 变更
- `protocols/*.md` 变更
- `guards/*.md` 变更

## 执行顺序

```
Step 1: 跑 T1 自检测试（12 题）
        全过 → Step 2 / 失败 → 回炉
Step 2: 跑 T2 红队测试（8 类 × 5 追问）
        全过 → Step 3 / 失败 → 回炉
Step 3: 跑 T3 功能测试（20 题抽 5）
        ≥ 4/5 过 → Step 4 / 失败 → 回炉
Step 4: 跑 T4 质量评分（抽 5 题按 rubric）
        每维 ≥ 4 分 + 每题 ≥ 20/25 → 通过 / 否则回炉
Step 5: 生成测试报告 → 归档 tests/results/YYYY-MM-DD-vN.md
Step 6: 允许发布新版本
```

## 执行方式

**MVP Phase 1**：纯人工执行。每次改 skill 后：
1. 开一个新的 Claude Code session
2. 按 T1 题目逐条喂给 skill，记录回答
3. 对照 Expected Behavior 打分
4. T2 需要多轮对话，按攻击序列操作
5. T3 抽 5 题跑完整对话
6. T4 用 T3 样本评分

**Phase 3+**：半自动化（见设计文档 §9.7）。

## 测试报告模板

保存到 `tests/results/YYYY-MM-DD-vN.md`：

```markdown
# Crux Test Report · vN

**日期**：YYYY-MM-DD
**版本**：v0.x.x
**测试人**：xxx

## T1 自检（12 题）
- 通过：N/12
- 失败项：题 X, X
- 详情：[链接或摘要]

## T2 红队（8 类）
- 通过：N/8 类
- 失败项：类 X 在第 N 次攻击时妥协

## T3 功能（5 题抽样）
- 通过：N/5
- 失败项：题 X

## T4 质量（5 题 × 5 维）
- 总分：M/125
- 最低维度：维度 X (平均 N 分)

## 结论
- ✅ 通过 M1 门槛 / ❌ 回炉
- 下一步：xxx
```

## 回炉流程

任一步失败 → 立即停测 → 根因分析：
- 是 Model 启发式不准？→ 改 models/*.md
- 是 Protocols 路径错？→ 改 protocols/*.md
- 是 Guards 禁令没触发？→ 改 guards/*.md
- 是 SKILL.md 人格设定弱？→ 改 SKILL.md

改完从 Step 1 重跑（不能只跑失败项，避免回归）。
