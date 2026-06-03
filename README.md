# study-note

A Claude Code skill for CS beginners who vibe code but want to actually learn.

After finishing a feature, run `/study-note` and get a personalized learning note saved to your project — written using your own code as the example.

## What it does

Analyzes your coding session (git diff + conversation context) and generates a structured note covering:

- What you built and why it works
- The technical concepts your code actually uses
- The "why" behind every key decision
- Bugs you hit and how you fixed them
- A quiz to test yourself
- A rebuild challenge to practice without AI

## Install

```
/skill install https://github.com/yihuang0830/skill.skill
```

Or add directly to your project's `.claude/skills/` directory.

## Usage

After finishing a feature:

```
/study-note login-feature
```

Or with no args — it infers the feature name from your git history:

```
/study-note
```

The note is saved to `docs/learning-notes/YYYY-MM-DD-<feature-name>.md`.

## Who this is for

You started coding in the era of AI assistants. You can ship things. But sometimes you finish a feature and realize you don't fully understand what you built.

This skill bridges that gap — it doesn't slow down your vibe coding, it just makes sure you walk away having actually learned something.

## Example output

See [example-note.md](docs/example-note.md) for a sample of what the generated notes look like.

## License

MIT
