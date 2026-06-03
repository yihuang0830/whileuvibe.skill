# study-note (`/sn`)

A Claude Code skill for CS beginners who vibe code but want to actually learn.

Not just a note-taker — a learning companion that teaches you while you build, checks your understanding mid-session, and generates a study note at the end.

## Install

```
/skill install https://github.com/yihuang0830/skill.skill
```

## Commands

| Command | When to use |
|---|---|
| `/sn on` | Start of a session — activates teaching mode |
| `/sn check` | Mid-session — quick 3-question quiz on your actual code |
| `/sn final` | End of session — generates a learning note |
| `/sn off` | Turn off teaching mode |

## What each command does

### `/sn on`
Activates teaching mode. From here on, Claude will:
- After every code block: add a 📚 "为什么这样写" explanation
- After every bug fix: add a 🐛 "根本原因" in plain language
- After every key decision: add a 💡 "为什么这么决定"
- Every 3–4 exchanges: ask a ✋ comprehension check

### `/sn check`
A quick mid-session quiz based on your actual code. 3 questions, one at a time, with feedback on each answer.

### `/sn final`
Generates a personalized learning note saved to `docs/learning-notes/YYYY-MM-DD-<feature>.md`, covering:
- What you built and why it works
- Technical concepts explained with your actual code as the example
- Data flow diagram
- Key design decisions and their reasoning
- Bugs you hit and how they got fixed
- Quiz questions
- A rebuild challenge to try without AI

### `/sn off`
Removes teaching mode. Claude goes back to normal.

---

## Who this is for

You started coding in the era of AI assistants. You can ship things. But sometimes you finish a feature and realize you don't fully understand what you built — you were just the one pressing Enter.

This skill fixes that. It doesn't slow down your vibe coding. It makes sure you actually understand what you're building as you build it.

## License

MIT
