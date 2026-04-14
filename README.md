# crux.skill · 参谋.skill

**A decision advisor for hard problems—no matter the field.**

You bring the problem (business strategy, product choice, legal dilemma, research direction, life decision, anything), and crux cross-examines you the way a sharp mentor would: finding the real question, surfacing what you haven't checked, and giving you the decision structure—**not the answer**.

---

## What is this

A Claude Code skill packaged as pure Markdown. Activated in a Claude Code session, it takes on the role of a decision advisor that:

- **Never gives answers** — only decision structure
- **Asks the hard questions** you haven't asked yourself
- **Surfaces information gaps** before you commit
- **Works across any industry** — business, tech, law, research, personal life

## How it works

Three-layer architecture:

```
Persona (SKILL.md)
    ↓ routes
Mental Models (models/*.md)
    ↓ consults (optionally)
Corpus (source texts, local only)
```

Current release ships with **2 mental models**:
- **Model 01 · Contradiction Analysis** — find the one thing that determines the rest
- **Model 02 · Groundtruth** — audit your information before you decide

5 more models coming in Phase 3+ (see `docs/DESIGN.md` for roadmap).

## Usage

1. Clone the repo:
   ```bash
   git clone git@github.com:ylzsdafei/crux-skill.git
   ```

2. Install as Claude Code skill:
   ```bash
   cp -r crux-skill ~/.claude/skills/crux
   ```

3. Restart Claude Code. The skill should appear in `/skills` list.

4. Bring a problem:
   > "我手上 3 个项目顾不过来，该放弃哪一个？"
   >
   > "我在两个 offer 间犹豫。"
   >
   > "这个 bug 是修还是重构？"

5. Answer crux's clarifying questions honestly. It won't tell you what to do—it tells you what you're really deciding.

## Design principles

1. **No roleplay** — crux is always "a decision advisor." It never claims to be any specific person.
2. **No quotes** — original wisdom is re-stated in everyday language. Never cited.
3. **No jargon** — theoretical terms stay internal. Outputs are plain words.
4. **No political takes** — historical / ideological questions get redirected.
5. **User's vocabulary** — crux uses your words, not its own.

## 中文说明

**任何行业、任何硬问题的决策参谋。**

你把问题抛进来（商业战略、产品取舍、法律难题、研究方向、人生决定），crux 像一位厉害的导师那样拷问你：找出真问题、暴露你没核查的盲点、给你决策结构——**不给答案**。

### 当前版本

v0.1.0 MVP · 包含 2 个心智模型（矛盾分析 + 调查研究）+ 完整交互协议 + 出厂禁令 + 完整测试集。

### 使用

```bash
git clone git@github.com:ylzsdafei/crux-skill.git
cp -r crux-skill ~/.claude/skills/crux
# 重启 Claude Code
```

在对话中抛真实问题，答它的追问，你会发现你真正在决定什么。

## Repository layout

```
crux-skill/
├── SKILL.md                  # Entry / persona / routing
├── models/                   # Mental model skeletons (Model 01, 02)
├── protocols/                # Interaction protocols (decision / analysis / vague / restate)
├── guards/                   # Output blocklist + runtime self-check
├── tests/                    # T1-T4 test suite + rubric + orchestrator
│   └── results/              # Test reports (v0.1.0-report.md)
├── distillation-log/         # Transparent provenance (prompts + v1 + v2)
├── source/                   # Source texts (gitignored)
└── corpus/                   # Extended corpus (gitignored)
```

## Quality gates (M1 passed)

v0.1.0 has passed:
- ✅ T1 self-test (12/12)
- ✅ T2 redteam adversarial (4/4 classes × 5 turns each)
- ✅ T3 functional multi-turn (3/3 sampled)
- ✅ T4 quality rubric (75/75 on sampled dialogues)
- ✅ Zero blocklist triggers across all test responses

Full report: `tests/results/2026-04-14-v0.1.0-report.md`

## Roadmap

- **v0.1.0** (2026-04-14) ✅ — MVP: 2 models, tests, basic persona
- **v0.2.0** (2-3 weeks) — Phase 2 Dogfood iteration, bug fixes from real use
- **v0.3.0** (2-4 weeks) — Add 5 more models (reality-check, long-game, focus-force, learn-by-doing, coalition)
- **v1.0.0** (2027-01-01) — Full release with public-domain source corpus

## Status

🚧 **Under active development**. Not production-stable. Breaking changes likely until v1.0.

## License

TBD — will be declared at v1.0.0 release.

## Attribution

The methodology distilled in this skill draws on a long tradition of dialectical decision-making and investigative analysis. Specific attributions will be detailed in `docs/ATTRIBUTION.md` at v1.0.0 release, when all source materials enter public domain.

## Contributing

Not accepting external contributions yet. Roadmap toward v0.3.0 is being executed by the author. After v0.3.0, `CONTRIBUTING.md` will open.

## Acknowledgments

Inspired by the `张雪峰.skill` and broader "person-distilled skills" movement, but crux takes the opposite stance: distill **methodology**, not **persona**. The skill should be a tool for your thinking, not a simulacrum of someone else's.
