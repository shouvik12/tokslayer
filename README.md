# ⚔️ tokslayer

> **Slays tokens before they compound in your session.**

You paste a GitHub README. Claude gets 4,600 tokens of nav chrome, boilerplate, and filler.  
Tokslayer intercepts. Claude gets 1,200 tokens of pure signal.

```
ORIGINAL:  "Skip to content shouvik12 trooper Repository navigation..."  (~4,600 tokens)
OPTIMIZED: "Trooper: LLM proxy. Local-first. Ollama default, Claude on escalate..."  (~1,200 tokens)
SAVED:     ~3,400 tokens (74%)
```

```
ORIGINAL:  "License: CC BY 4.0 arXiv:2504.15989v2 [cs.SE] 29 May 2025..."  (~4,800 tokens)
OPTIMIZED: "Paper: LLMs use CoT for code repair, but CoT inflates token use..."  (~1,900 tokens)
SAVED:     ~2,900 tokens (60%)
```

**Same answer. Fraction of the cost.**

---

## You're doing this right now without knowing it

Every time you copy a webpage, a README, a doc page — your clipboard picks up everything. Navigation. Footers. Boilerplate. License text. Share buttons rendered as text. Metadata. All of it lands in Claude's context window.

You wanted the content. Claude got the garbage too. And you paid for every token of it.

Tokslayer slays the garbage before Claude sees it. You don't change how you work. You just stop paying for the noise.

---

## The problem nobody talks about

Everyone optimizes what they *type*. Nobody optimizes what they *paste*.

But developers paste constantly:

- GitHub READMEs
- Research papers
- API documentation
- Jira tickets
- Confluence pages
- Stack Overflow answers
- Slack threads
- PR descriptions
- Emails

All of it written for humans — verbose, padded, full of nav chrome and filler. Claude reads every token. You pay for every token.

**Your clipboard is leaking tokens. Tokslayer slays them.**

---

## Install

One file. Drop it in. Done.

```bash
# macOS / Linux
curl -fsSL https://raw.githubusercontent.com/shouvik12/tokslayer/main/install.sh | bash
```

Or manually:

```bash
mkdir -p ~/.claude/skills/tokslayer
curl -o ~/.claude/skills/tokslayer/SKILL.md \
  https://raw.githubusercontent.com/shouvik12/tokslayer/main/.claude/skills/tokslayer/SKILL.md
```

Restart Claude Code. Tokslayer activates on every session automatically.

---

## How it works

No proxy. No binary. No server. No MCP.

Just a `SKILL.md` that Claude Code reads on startup. Claude itself detects pasted content, compresses it using cl100k_base-aligned vocabulary, and responds to your command using the optimized version.

```
You paste doc + type "explain"
           ↓
Tokslayer detects pasted content
           ↓
Strips nav chrome, filler, verbose phrases
           ↓
Replaces with shortest equivalent words (cl100k_base single-token merges)
           ↓
Claude responds to compressed version — shorter, more focused output
           ↓
Compressed version stays in session history — every subsequent turn costs less
```

**What gets slayed:**
- Navigation chrome that came along with the copy
- Filler phrases ("aforementioned", "in order to", "is responsible for")
- Redundant sentences that repeat the same point
- Marketing language and legal boilerplate
- Verbose corporate speak

**What stays untouched:**
- Code blocks
- Stack traces
- URLs and file paths
- Numbers and metrics
- Technical terms
- Proper nouns

---

## Benchmarks

Real token counts from live Claude Code sessions.

| Content | Original | Optimized | Saved |
|---|---|---|---|
| GitHub README (trooper) | 4,600 | 1,200 | **74%** |
| Research paper (arXiv) | 4,800 | 1,900 | **60%** |
| GitHub README (caveman) | 1,800 | 600 | **67%** |
| API documentation | 105 | 35 | **67%** |
| **Average** | | | **67%** |

Note: these savings are on output tokens and session history. Claude responds to the compressed version, and the compressed version stays in context across all subsequent turns. Write-path interception for true input token saving is on the roadmap.

---

## Works with

- Claude Code ✅
- Any agent that reads `SKILL.md` ✅

---

## Part of the same army as

| Repo | What |
|---|---|
| [**trooper**](https://github.com/shouvik12/trooper) | Routes Claude → Ollama fallback. Keeps you running when quota runs out. |
| [**tokslayer**](https://github.com/shouvik12/tokslayer) | Slays clipboard bloat before it reaches Claude. |

Trooper handles the routing. Tokslayer handles the input. Together: lower cost, longer sessions, faster responses.

---

## License

MIT — slay freely.
