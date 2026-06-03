# whileuvibe (`/yuv`) — you understand vibing

**English** | [中文](#中文)

A Claude Code skill for CS beginners who vibe code but want to actually learn.

Not just a note-taker — a learning companion that teaches you while you build, checks your understanding mid-session, and generates a study note at the end. Fully bilingual: detects your language and responds accordingly.

## Install

```
/skill install https://github.com/yihuang0830/whileuvibe.skill
```

## Commands

| Command | When |
|---|---|
| `/yuv on` | Start of session — activates teaching mode |
| `/yuv check` | Mid-session — 3-question quiz on your actual code |
| `/yuv final` | End of session — generates a learning note |
| `/yuv off` | Deactivate teaching mode |

## What each command does

**`/yuv on`** — Activates teaching mode. Claude will:
- After every code block → 📚 "Why this works"
- After every bug fix → 🐛 "Root cause"
- After every key decision → 💡 "Why this decision"
- Every 3–4 exchanges → ✋ comprehension check: "explain this in your own words"

**`/yuv check`** — 3 questions based on your actual code, one at a time, with feedback.

**`/yuv final`** — Saves a learning note to `docs/learning-notes/YYYY-MM-DD-<feature>.md` covering: concepts with your real code as examples, data flow, design decisions, bugs, quiz questions, and a rebuild challenge.

**`/yuv off`** — Removes teaching mode.

---

## Who this is for

You started coding in the AI era. You can ship things. But sometimes you finish a feature and realize you don't fully understand what you built.

This skill fixes that. It doesn't slow down your vibe coding — it makes sure you actually understand what you're building as you build it.

---

---

## 中文

# whileuvibe (`/yuv`)

[English](#whileuvibe-yuv) | **中文**

一个专为 vibe coding 新手设计的 Claude Code skill。

不只是生成笔记——在你写代码的过程中帮你真正学懂：边写边解释、随时检验理解、最后生成一份专属你的学习笔记。自动识别语言，中英文都支持。

## 安装

```
/skill install https://github.com/yihuang0830/whileuvibe.skill
```

## 命令

| 命令 | 时机 |
|---|---|
| `/yuv on` | 开始写代码前——开启教学模式 |
| `/yuv check` | 随时——用你自己的代码测一测 |
| `/yuv final` | 写完一个功能——生成学习笔记 |
| `/yuv off` | 关闭教学模式 |

## 每个命令做什么

**`/yuv on`** — 开启教学模式。之后 Claude 会：
- 每写完一段代码 → 📚「为什么这样写」
- 每修完一个 bug → 🐛「根本原因」
- 每做一个设计决策 → 💡「为什么这么决定」
- 每 3–4 轮对话 → ✋ 理解检查：「用你自己的话解释一下……」

**`/yuv check`** — 基于你实际代码出 3 道题，一题一题来，每题有反馈。

**`/yuv final`** — 把学习笔记存到 `docs/learning-notes/YYYY-MM-DD-功能名.md`，包含：用你的真实代码讲解的概念、数据流图、设计决策、遇到的 bug、quiz 题目、不用 AI 的重建挑战。

**`/yuv off`** — 关闭教学模式。

## 给谁用的

你生在了好年代，一开始学 CS 就可以 vibe coding。你能写出东西，但有时候功能跑通了，回头一看——其实不太懂自己写了什么。

这个 skill 就是为了解决这个问题。不会拖慢你的节奏，只是让你在 vibe 的过程中真的学到点东西。

## License

MIT
