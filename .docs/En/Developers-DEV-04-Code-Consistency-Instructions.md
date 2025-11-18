# Code Consistency and Instruction Files

**ID:** DEV-04  
**Platform:** GitHub Enterprise + Setup  

## Target Audience
Developers

## AI Used
GitHub Enterprise

## AI Knowledge Level
Intermediate

## Technical Summary
Use instruction files in the .github repository to maintain code consistency and guide AI in generating code that conforms to team standards.

## Content

Excellent question 👏 — you're touching on an **advanced and little-known part of GitHub Copilot Enterprise**, related to **customizing Copilot's behavior** through instruction files in the `.github` repository.

Here's a clear and technical explanation of each file:

---

## 🧩 **1. `.github/copilot-instructions.md`**

### 📘 **Purpose:**

This is **the master global instructions file** for GitHub Copilot in a repository.
It allows you to **influence how Copilot generates code, comments, or documents**, for the entire team.

### ⚙️ **How it works:**

- Copilot reads this file **when suggesting code** or responding in Copilot Chat.
- The content acts as a **permanent context layer**, similar to *Custom Instructions* in ChatGPT.

### 🧠 **Typical usage:**

You define:

- **Code standards** (language, style, docstring, comment format).
- **Naming conventions** (variables, functions, files).
- **Team or project-specific best practices**.
- **Behaviors to avoid** (e.g. "don't suggest untyped code", "avoid print() in libs").

### 💡 **Concrete example:**

```markdown
# .github/copilot-instructions.md

## Code style
- Use snake_case functions.
- Always include a Google-format docstring.
- Use f-strings for logs.

## Tests
- Suggest unit tests with pytest.
- Prefer unittest library for integration tests.

## Security
- Never include passwords, API keys, or tokens in generated code.
```

🧩 **Result:**
Copilot automatically adjusts its suggestions according to these directives in **all repository files**.
This is ideal for **standardizing practices among multiple developers.**

---

## 🧩 **2. `.github/instructions/**/NAME.instructions.md`**

### 📘 **Purpose:**

These files serve to **define specific contextual instructions** for **precise domains** of the project.

They are more **granular** than the main file, and allow adapting behaviors to subdirectories, modules or task types.

### 🧠 **Typical structure:**

- The `instructions/` folder can contain several subdirectories (e.g. `frontend/`, `backend/`, `devops/`).
- Each `.instructions.md` file has a **clear name** (e.g. `api.instructions.md`, `tests.instructions.md`).

### 💡 **Concrete example:**

```
.github/instructions/backend/api.instructions.md
```

Content:

```markdown
# API Instructions
- Use FastAPI for endpoints.
- Functions must return a JSON object.
- Prefer async/await for all routes.
- Add a docstring with response schema.
```

✅ **Effect:**
When you code in `/backend/`, Copilot **prioritizes these directives** over those in the global file.

This allows having:

- Different style for backend vs frontend.
- Conventions adapted to technologies (React vs Python, etc.).
- Distinct rules according to modules.

---

## 🧩 **3. `.github/<agent>`**

### 📘 **Purpose:**

This directory concerns **Copilot Agents** — specialized assistants integrated into GitHub Copilot Chat (introduced with Copilot Enterprise).

Each "agent" acts as a **personalized AI role**:

- `copilot`, `security`, `docs`, `tests`, etc.

These agents can be configured to respond differently according to their mission.

### ⚙️ **Example structure:**

```
.github/
 ├── copilot-instructions.md
 ├── instructions/
 │    └── backend/api.instructions.md
 └── agents/
      ├── security/
      │    └── security.instructions.md
      ├── docs/
      │    └── docs.instructions.md
```

### 💡 **Agent usage examples:**

#### `.github/agents/security/security.instructions.md`

```markdown
# Copilot security agent
- Prioritize vulnerability detection.
- Never ignore critical dependency alerts.
- Prefer using "secrets" library for keys.
```

#### `.github/agents/docs/docs.instructions.md`

```markdown
# Documentation agent
- Generate README in Markdown format.
- Use professional, concise and clear tone.
- Add minimal usage example for each public function.
```

### 🚀 **Effect:**

When a user discusses with Copilot Chat and calls an agent (e.g. `/security` or `/docs`),
Copilot **automatically reads the corresponding instructions** to adjust its behavior.

---

## 🔐 **Global summary**

| **Location**                                | **Scope**                          | **Main utility**                                       |
| ------------------------------------------- | ---------------------------------- | ------------------------------------------------------ |
| `.github/copilot-instructions.md`          | Global (entire repo)               | Standardize code and style practices.                  |
| `.github/instructions/**/NAME.instructions.md` | Contextual (by module / folder) | Adapt Copilot to specific project areas.               |
| `.github/agents/**/NAME.instructions.md`   | Copilot Chat agent (dedicated role) | Specialize AI assistants (docs, security, tests, etc.). |

---

Would you like me to create a **complete example .github/ structure** with all these files (and their minimal content) for your GitHub Enterprise demo repository?
👉 I could generate it as a **zip file** ready to drop in a repo.

## Summary

This article explains how to use GitHub Enterprise's advanced instruction file system to customize Copilot's behavior and maintain code consistency across teams.

**Key components:**
- **Global instructions**: `.github/copilot-instructions.md` for repository-wide standards
- **Contextual instructions**: Folder-specific guidance for different project areas
- **Specialized agents**: Role-based AI assistants for security, documentation, testing

**Benefits:**
- **Consistent code quality** across all team members
- **Context-aware suggestions** adapted to specific project areas
- **Specialized assistance** through dedicated AI agents
- **Scalable governance** for large development teams

This system transforms Copilot from a generic code assistant into a **customized team member** that understands and enforces your specific development standards.