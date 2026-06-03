# study-note

A Claude Code skill for CS beginners who vibe code but want to actually learn.

Not just a note-taker — a learning companion that teaches you while you build, checks your understanding mid-session, and generates a study note at the end.

## Install

```
/skill install https://github.com/yihuang0830/skill.skill
```

## How to use

### At the start of a session

```
/study-note on
```

Activates teaching mode. From here on, Claude will:
- After every code block: add a 📚 "为什么这样写" explanation
- After every bug fix: add a 🐛 "根本原因" in plain language
- After every key decision: add a 💡 "为什么这么决定"
- Every 3–4 exchanges: ask a ✋ comprehension check — "用你自己的话说说这个函数是干什么的？"

### During the session (anytime)

```
/study-note check
```

A quick mid-session quiz based on your actual code. 3 questions, one at a time, with feedback.

### At the end of the session

```
/study-note login-feature
```

Generates a personalized learning note saved to `docs/learning-notes/YYYY-MM-DD-login-feature.md`, covering:
- What you built and why it works
- Technical concepts explained with your actual code as the example
- Data flow diagram
- Key design decisions and their reasoning
- Bugs you hit and how they got fixed
- Quiz questions
- A rebuild challenge to try without AI

### To turn off teaching mode

```
/study-note off
```

---

## Who this is for

You started coding in the era of AI assistants. You can ship things. But sometimes you finish a feature and realize you don't fully understand what you built — you were just the one pressing Enter.

This skill fixes that. It doesn't slow down your vibe coding. It makes sure you actually understand what you're building as you build it.

## License

MIT
