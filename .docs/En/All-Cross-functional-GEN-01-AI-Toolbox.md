# Creating Your Team AI Toolbox

**ID:** GEN-01  
**Platform:** ChatGPT + GitHub + Custom Prompts  

## Target Audience
All / Cross-functional

## AI Used
ChatGPT/MS Copilot

## AI Knowledge Level
Intermediate

## Technical Summary
Build a library of prompts, templates and automations adapted to your work environment to maximize team efficiency with AI.

## Content

### 1. Introduction: Why an AI Toolbox?

A team AI Toolbox is an organized and standardized collection of AI tools, prompts and processes that allows all team members to:
- **Save time** by reusing proven prompts
- **Maintain consistency** in AI usage
- **Capitalize on collective experience**
- **Facilitate AI adoption** by everyone

### 2. Audit and needs inventory

#### 2.1 Use case mapping
**Practical exercise:** Organize a team workshop (2h) to identify:

| Role/Position | Repetitive tasks | AI tools used | Favorite prompts |
|---------------|------------------|---------------|------------------|
| Developer | Code review, documentation | GitHub Copilot, ChatGPT | To document |
| QA | Test cases, bug reports | ChatGPT | To document |
| PM/SM | User stories, planning | ChatGPT, Notion AI | To document |
| HR | CV analysis, emails | ChatGPT | To document |

#### 2.2 Individual audit questionnaire
```
1. What AI tools do you currently use?
2. How frequently? (daily/weekly/monthly)
3. For which specific tasks?
4. What are your most effective prompts?
5. What difficulties do you encounter?
6. What would you like to automate/improve?
```

### 3. Toolbox structure

#### 3.1 Organization by categories
```
📁 AI-Toolbox/
├── 📁 Development/
│   ├── code-review-prompts.md
│   ├── documentation-templates.md
│   └── debugging-assistants.md
├── 📁 QA-Test/
│   ├── test-case-generation.md
│   ├── bug-analysis-prompts.md
│   └── automated-testing.md
├── 📁 Management/
│   ├── user-stories-templates.md
│   ├── planning-assistants.md
│   └── meeting-summaries.md
├── 📁 HR-Recruitment/
│   ├── cv-analysis-prompts.md
│   ├── interview-prep.md
│   └── job-description-templates.md
└── 📁 Common/
    ├── email-templates.md
    ├── presentation-helpers.md
    └── research-prompts.md
```

#### 3.2 Standard template for each prompt

**Recommended structure:**

```markdown
# [Prompt Name]

## Objective
Clear description of what the prompt does

## Usage context
When and why to use it

## Prompt Template
[Your prompt here with variables {{variable}}]

## Usage example
Concrete input and expected output

## Variants
Adaptations according to context

## Metrics
- Time saved: X minutes
- Efficiency: X/10
- Last update: DATE
```

### 4. Creating standardized prompts

#### 4.1 Universal prompts (all roles)

**📝 Professional email**
```
Rewrite this email to make it more professional, concise and benevolent:

[YOUR EMAIL DRAFT]

Context: {{relationship_context}} (hierarchical/colleague/client)
Desired tone: {{formal/friendly/urgent}}
```

**📊 Meeting summary**
```
Transform these meeting notes into a structured report:

[YOUR NOTES]

Desired format:
- Participants
- Key points discussed
- Decisions made
- Action items (who/what/when)
- Next steps
```

**🔍 Problem analysis**
```
Analyze this problem and propose solutions:

Problem: {{problem_description}}
Context: {{business_context}}
Constraints: {{technical/budget/time_constraints}}

Structure your response:
1. Problem analysis
2. Probable causes
3. 3 solutions with pros/cons
4. Justified recommendation
```

#### 4.2 Role-specific prompts (examples)

**💻 Development - Code Review**
```
Analyze this code and give constructive feedback:

[CODE TO ANALYZE - Language: {{language}}]
{{code_to_review}}

Focus on:
- Readability and maintainability
- Potential performance
- Security
- {{language}} best practices
- Improvement suggestions

Format: Positive points | Points to improve | Suggestions
```

**🔬 QA - Test case generation**
```
Generate test cases for this feature:

Feature: {{feature_description}}
Acceptance criteria: {{criteria}}
Environment: {{web/mobile/API}}

For each test case, include:
- Unique ID
- Prerequisites
- Test steps
- Expected result
- Priority (High/Medium/Low)

Include positive, negative and edge test cases.
```

### 5. Maintenance and evolution process

#### 5.1 Toolbox governance
- **Toolbox Owner**: Designate a guardian per team
- **Monthly review**: Evaluate prompts and add new ones
- **Collective feedback**: Dedicated channel to share feedback
- **Versioning**: Version numbering for prompts

#### 5.2 Success metrics
```
📊 Monthly dashboard:
- Number of active users
- Most used prompts
- Average time saved per prompt
- User satisfaction (1-10)
- New prompts created
- Improvements made
```

#### 5.3 Continuous improvement process
1. **Feedback collection**: Simple form after usage
2. **Usage analysis**: Which prompts are abandoned/used
3. **Optimization**: Improvement of existing prompts
4. **Innovation**: New use cases identified
5. **Training**: Experience sharing sessions

### 6. Training and adoption

#### 6.1 Deployment plan (4 weeks)
**Week 1: Awareness**
- Concept presentation (30 min)
- Demonstration with concrete examples
- Formation of teams by role

**Week 2: Co-creation**
- Workshops by role (1h30 each)
- Creation of first prompts
- Testing and validation in pairs

**Week 3: Practice**
- Encouraged daily use
- Individual support available
- Collection of first feedback

**Week 4: Consolidation**
- Collective experience feedback
- Adjustments and improvements
- Planning next steps

#### 6.2 Adoption support
- **AI Champions**: Identify ambassadors per team
- **Quick wins**: Start with simple use cases
- **Guidance**: Individual support in first weeks
- **Gamification**: Points/badges system for usage

### 7. Security and best practices

#### 7.1 Security guidelines
⚠️ **NEVER share with AI:**
- Customer personal data
- Access codes/passwords
- Confidential project information
- Sensitive proprietary code

✅ **Best practices:**
- Anonymize data in examples
- Use fictional data for tests
- Validate outputs before use
- Respect company policy

#### 7.2 Prompt validation checklist
```
□ Is the prompt clear and unambiguous?
□ Are variables well defined?
□ Is the usage example relevant?
□ Does it respect security policy?
□ Has it been tested by at least 2 people?
□ Is documentation complete?
```

### 8. Ready-to-use template examples

#### 8.1 Incident report template
```
Analyze this incident and propose an action plan:

Incident: {{description}}
Time: {{timestamp}}
Impact: {{affected_users}}
Systems involved: {{systems}}

Generate:
1. Timeline of events
2. Estimated business impact
3. Probable causes (technical/process/human)
4. Immediate corrective actions
5. Prevention plan
6. Proposed communication
```

#### 8.2 Competitive analysis template
```
Analyze this competitor and compare with our solution:

Competitor: {{competitor_name}}
Product/Service: {{description}}
Our context: {{our_product}}

Analysis:
1. Competitor strengths
2. Identified weaknesses
3. Differentiation vs our offering
4. Opportunities for us
5. Threats to anticipate
6. Strategic recommendations
```

### 9. Tools and integrations

#### 9.1 Recommended tech stack
- **Storage**: GitHub/GitLab for versioning
- **Documentation**: Notion/Confluence/Wiki
- **Sharing**: Slack/Teams with dedicated channels
- **Metrics**: Simple dashboard (Excel/Google Sheets)

#### 9.2 Possible integrations
- **Slack bots**: Prompts accessible via commands
- **Browser extensions**: Quick access to templates
- **API integrations**: Automation with existing tools

### 10. Roadmap and evolution

#### 10.1 Phase 1 (Months 1-2): Foundations
- Create basic structure
- 20 essential prompts
- Initial team training
- Basic processes established

#### 10.2 Phase 2 (Months 3-4): Expansion
- 50+ specialized prompts
- Integrations with existing tools
- Metrics and dashboard
- Active user community

#### 10.3 Phase 3 (Months 5-6): Optimization
- Role-specialized AI
- Advanced automations
- Continuous training
- Inter-team sharing

## Summary

Creating an effective team AI Toolbox requires:

1. **Precise audit** of current needs and usage
2. **Clear structure** that is scalable for organizing resources
3. **Standardized templates** facilitating reuse
4. **Governance process** to maintain quality
5. **Progressive adoption plan** with support
6. **Metrics** to measure impact and improvement

**Expected benefits:**
- ⏱️ **Time savings**: 20-30% on repetitive tasks
- 🎯 **Improved quality**: More consistent and professional outputs
- 🤝 **Enhanced collaboration**: Sharing expertise and best practices
- 📈 **Skill development**: Progressive AI adoption by everyone

**Next steps:**
1. Present concept to management team
2. Identify early adopters
3. Organize first audit workshop
4. Create first prompts collaboratively
5. Launch 4-week pilot phase

The AI Toolbox thus becomes a strategic team asset, evolving with needs and capitalizing on collective intelligence to maximize AI impact in the organization.