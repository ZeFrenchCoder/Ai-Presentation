# Getting Started with AI in GitHub Enterprise

**ID:** DEV-01  
**Platform:** GitHub Enterprise + Setup  

## Target Audience
Developers

## AI Used
GitHub Enterprise

## AI Knowledge Level
Beginner

## Technical Summary
Configuration and AI tools integrated into GitHub to boost productivity and code quality.

## Content

### 🧠 Introduction – Putting AI at the service of the developer

Copilot is not a magic wand: it's a code partner.
It understands your context, anticipates your intention and suggests code that conforms to your style.

Copilot Chat becomes a "technical assistant" in your IDE: it explains, documents and generates tests on demand.

Together, these tools save time without sacrificing quality or security, as everything remains in your GitHub Enterprise environment.

### 🧪 Demonstration 1 — Creating a function with Copilot

#### 🎯 Goal
Show how a clear comment allows Copilot to generate complete and contextual code.

#### ⚙️ Technical Steps
1. Open a Python file (or JS, C#, etc.).

2. Write:
```python
# create a function that sorts a list of dictionaries by date
```

3. Observe the auto-completion suggested by Copilot:
```python
def sort_by_date(list):
    return sorted(list, key=lambda x: x['date'])
```

4. Accept the suggestion, then slightly modify the comment to see Copilot suggest a new version.

#### 💡 Key Points
- The more precise your comment, the more relevant the suggestion.
- Copilot understands functional intents (e.g. "sort", "calculate", "validate").

### 🧪 Demonstration 2 — Using Copilot Chat to explain and test

#### 🎯 Goal
Show how `/explain` and `/tests` transform Copilot Chat into a virtual mentor and tester.

#### ⚙️ Technical Steps
1. Select an existing function in your file.

2. Open Copilot Chat and type:
```
/explain
```

👉 Copilot gives you a clear explanation of what the function does, line by line.

3. Then ask:
```
/tests
```

👉 Copilot suggests a set of unit tests corresponding to this function.

4. Copy a test and run it locally to validate the behavior.

#### 💡 Key Points
- `/explain` is perfect for onboarding or code review.
- `/tests` accelerates unit coverage while keeping the existing code logic.
- AI doesn't replace developer judgment, it accelerates their iteration.

## Summary

This article presents GitHub Copilot as an **intelligent development partner** that understands context and anticipates developer intentions.

**Key Points:**
- **Copilot** generates code from precise comments and adapts to existing style
- **Copilot Chat** acts as a technical assistant with specialized commands (`/explain`, `/tests`)
- **Productivity gain** without compromising quality thanks to native GitHub Enterprise integration
- **Practical approach**: two concrete demonstrations to master the basics

**Result:** Developers can immediately improve their workflow by using AI as a virtual mentor that accelerates code writing, explanation and testing.

## Useful Links

### 📚 Official Documentation
- [GitHub Copilot Documentation](https://docs.github.com/en/copilot) - Complete official guide
- [GitHub Copilot Chat](https://docs.github.com/en/copilot/github-copilot-chat) - Copilot Chat documentation
- [GitHub Copilot for Business](https://docs.github.com/en/copilot/copilot-for-business) - Enterprise configuration

### 🎓 Training and Tutorials
- [GitHub Copilot Fundamentals](https://learn.microsoft.com/en-us/training/paths/copilot/) - Microsoft Learn
- [Getting Started with GitHub Copilot](https://github.blog/2022-06-21-github-copilot-is-generally-available-to-all-developers/) - GitHub Blog
- [Copilot Best Practices](https://github.blog/2023-06-20-how-to-write-better-prompts-for-github-copilot/) - Advanced techniques

### 🔧 Tools and Extensions
- [GitHub Copilot VS Code Extension](https://marketplace.visualstudio.com/items?itemName=GitHub.copilot) - Official extension
- [GitHub Copilot Chat Extension](https://marketplace.visualstudio.com/items?itemName=GitHub.copilot-chat) - Integrated chat
- [GitHub Copilot for IntelliJ](https://plugins.jetbrains.com/plugin/17718-github-copilot) - JetBrains support

### 📖 Additional Resources
- [Awesome GitHub Copilot](https://github.com/sindresorhus/awesome-github-copilot) - Resource collection
- [Copilot Patterns](https://github.com/microsoft/copilot-patterns) - Microsoft patterns and examples
- [Enterprise Setup Guide](https://docs.github.com/en/enterprise-cloud@latest/copilot/managing-copilot-for-business) - Enterprise configuration