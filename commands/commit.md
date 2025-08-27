---
description: Generate and execute git commit with AI-generated message
allowed_tools: ["Bash"]
---

!git status
!git diff --staged

Analyze the staged changes and generate an appropriate commit message following conventional commit format. Consider:
- Type of changes (feat, fix, docs, style, refactor, test, chore)
- Scope if applicable
- Clear, concise description
- Breaking changes if any

Then execute the git commit with the generated message using:
```
git commit -m "your-generated-message"
```

🤖 Generated with [Claude Code](https://claude.ai/code)

Co-Authored-By: Keboom <keboom777@gmail.com>
