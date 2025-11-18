# AI-Assisted Planning and Prioritization

**ID:** PO-01  
**Platform:** ChatGPT + Agile Planning Tools  

## Target Audience
Scrum Master / Product Owner

## AI Used
ChatGPT/MS Copilot

## AI Knowledge Level
Intermediate

## Technical Summary
Use AI to optimize sprint planning, backlog prioritization, and capacity planning for improved team productivity.

## Content

### 🧠 Introduction – AI in Agile Planning

AI can transform agile planning by:
- **Analyzing backlog items** for complexity and dependencies
- **Optimizing sprint capacity** based on team velocity
- **Identifying risks** in sprint commitments
- **Suggesting story breakdowns** for better estimation

### 🧪 Demonstration 1 — Backlog Prioritization Analysis

#### 🎯 Goal
Use AI to analyze and prioritize product backlog items based on multiple criteria.

#### ⚙️ Technical Steps

1. **Present backlog items to AI for analysis**:
```
Analyze and prioritize these product backlog items:

User Stories:
1. "As a user, I want to reset my password so I can regain access to my account"
   - Business Value: High security requirement
   - Effort: 3 story points
   - Dependencies: Email service integration

2. "As an admin, I want to export user data to CSV so I can analyze usage patterns"
   - Business Value: Analytics capability
   - Effort: 5 story points  
   - Dependencies: Database optimization

3. "As a user, I want dark mode so I can use the app comfortably at night"
   - Business Value: User experience enhancement
   - Effort: 8 story points
   - Dependencies: UI component updates

4. "As a customer, I want to save payment methods so I can checkout faster"
   - Business Value: Conversion optimization
   - Effort: 13 story points
   - Dependencies: Payment gateway security, PCI compliance

Current Context:
- Team velocity: 25 story points per sprint
- Security audit due in 2 sprints
- Major customer requesting faster checkout

Provide prioritization with rationale.
```

2. **AI provides prioritized analysis**:
```markdown
## Backlog Prioritization Analysis

### 🥇 Priority 1: Password Reset Feature
**Rationale:**
- **Security Critical:** Essential for user account security
- **Low Effort, High Impact:** 3 points for high business value
- **Risk Mitigation:** Required for upcoming security audit
- **User Blocker:** Users currently locked out cannot self-recover

**Sprint Recommendation:** Include in current sprint

### 🥈 Priority 2: Save Payment Methods  
**Rationale:**
- **Revenue Impact:** Direct conversion optimization for major customer
- **Strategic Value:** Addresses specific customer requirement
- **Complexity Management:** 13 points requires careful planning
- **Technical Debt:** Payment security needs thorough implementation

**Sprint Recommendation:** Start in next sprint, split into smaller stories

### 🥉 Priority 3: CSV Export Feature
**Rationale:**
- **Business Intelligence:** Enables data-driven decisions
- **Medium Effort:** 5 points fits well in sprint planning
- **Internal Tool:** Important but not customer-facing
- **Database Dependency:** Requires coordination with infrastructure team

**Sprint Recommendation:** Sprint 3-4 timeframe

### 4️⃣ Priority 4: Dark Mode
**Rationale:**
- **Nice-to-Have:** User experience enhancement
- **High Effort:** 8 points for non-critical feature
- **UI Overhaul:** Touches many components, high regression risk
- **Lower ROI:** Significant effort for aesthetic improvement

**Sprint Recommendation:** Consider for future quarter after critical features

### 📊 Suggested Sprint Distribution
**Sprint 1 (Current):** Password Reset (3pts) + smaller items (22pts available)
**Sprint 2:** Begin Payment Methods (break into 8pt + 5pt stories)
**Sprint 3:** Complete Payment Methods + CSV Export
**Sprint 4:** Dark Mode (if capacity permits)
```

### 🧪 Demonstration 2 — Sprint Capacity Planning

#### 🎯 Goal
Optimize sprint planning using AI analysis of team capacity and story complexity.

#### ⚙️ Technical Steps

1. **Provide team capacity data for analysis**:
```
Plan optimal sprint commitment with this team data:

Team Composition:
- 2 Senior Developers (8 hours/day each)
- 2 Junior Developers (6 productive hours/day each)  
- 1 UI/UX Developer (7 hours/day)
- 1 QA Engineer (8 hours/day)

Sprint Constraints:
- 10-day sprint
- 1 senior dev on vacation for 3 days
- New junior dev (50% productivity first sprint)
- Holiday on Friday (team unavailable)

Story Estimates:
- User Authentication: 8 points (backend heavy)
- Payment Gateway: 13 points (full-stack + security)
- Dashboard UI: 5 points (frontend focused)
- Bug fixes: 3 points (mixed skills)
- API Documentation: 2 points (backend)

Calculate realistic capacity and recommend sprint contents.
```

2. **AI calculates optimal sprint plan**:
```markdown
## Sprint Capacity Analysis

### 👥 Available Capacity Calculation

**Senior Developers:**
- Developer 1: 9 days × 8 hours = 72 hours
- Developer 2: 6 days × 8 hours = 48 hours (vacation adjustment)
- **Total Senior Capacity:** 120 hours

**Junior Developers:**
- Developer 1: 9 days × 6 hours = 54 hours
- Developer 2: 9 days × 3 hours = 27 hours (50% productivity)
- **Total Junior Capacity:** 81 hours

**Specialists:**
- UI/UX Developer: 9 days × 7 hours = 63 hours
- QA Engineer: 9 days × 8 hours = 72 hours

**Total Team Capacity:** 336 productive hours

### 📊 Story Point to Hour Conversion
Based on team velocity: **1 story point ≈ 11 hours**
**Realistic Sprint Capacity:** 30 story points (with 10% buffer)

### 🎯 Recommended Sprint Commitment

**Tier 1 - Must Have (18 points):**
- User Authentication: 8 points
  - *Rationale: Security priority, senior dev availability*
- Dashboard UI: 5 points  
  - *Rationale: Leverages UI/UX specialist*
- Bug fixes: 3 points
  - *Rationale: Quick wins, shared across team*
- API Documentation: 2 points
  - *Rationale: Good task for junior developer learning*

**Tier 2 - If Capacity Allows (13 points):**
- Payment Gateway: 13 points
  - *Rationale: High complexity, requires both senior devs*

### ⚠️ Risk Assessment
- **Medium Risk:** Junior developer productivity unknown
- **Low Risk:** Senior dev vacation planned and accounted for
- **Mitigation:** Start Payment Gateway only if Tier 1 progressing well

### 📅 Daily Capacity Distribution
- **Days 1-3:** Focus on Authentication (senior dev available)
- **Days 4-6:** UI work + junior dev tasks
- **Days 7-9:** Integration and testing
- **Final Day:** Buffer for completion and retrospective prep
```

### 🧪 Demonstration 3 — Risk Identification and Mitigation

#### 🎯 Goal
Use AI to identify potential risks in sprint planning and suggest mitigation strategies.

#### ⚙️ Technical Steps

1. **Present sprint plan for risk analysis**:
```
Analyze this sprint plan for potential risks:

Sprint Goal: "Complete user onboarding flow"

Committed Stories:
- User Registration API (5 points) - depends on email service
- Email Verification System (8 points) - new integration
- Profile Setup UI (3 points) - needs design approval  
- Password Strength Validation (2 points) - security compliance
- Welcome Email Template (1 point) - marketing review needed

Team Status:
- New team working together for first time
- External dependency on email service provider
- Design team overloaded this sprint
- Security review process takes 2-3 days minimum

Identify risks and suggest mitigation strategies.
```

2. **AI provides comprehensive risk analysis**:
```markdown
## Sprint Risk Analysis

### 🚨 High Risk Issues

**1. External Email Service Dependency**
- **Impact:** Blocks 13 points (Registration + Verification)
- **Probability:** Medium (external service delays common)
- **Mitigation Strategies:**
  - Start email service integration immediately
  - Create mock service for parallel development
  - Have backup email provider ready
  - Daily check-ins with service provider

**2. Design Approval Bottleneck**
- **Impact:** Blocks 3 points (Profile Setup UI)
- **Probability:** High (design team overloaded)
- **Mitigation Strategies:**
  - Get design approval before sprint starts
  - Create low-fidelity mockups for development
  - Schedule dedicated design review session
  - Have fallback simple design ready

### ⚠️ Medium Risk Issues

**3. Security Review Timeline**
- **Impact:** Delays 2 points + potential rework
- **Probability:** Medium (review process unpredictable)
- **Mitigation Strategies:**
  - Submit password validation for early review
  - Involve security team in planning
  - Use established security patterns
  - Plan review in previous sprint

**4. New Team Collaboration**
- **Impact:** Potential velocity reduction
- **Probability:** Medium (team dynamics unknown)
- **Mitigation Strategies:**
  - Daily standups with focus on blockers
  - Pair programming for knowledge sharing
  - Clear communication protocols
  - Regular pulse checks on team dynamics

### 🔧 Recommended Mitigation Plan

**Pre-Sprint Actions:**
- [ ] Initiate email service setup (Dev Lead)
- [ ] Schedule urgent design review (Product Owner)
- [ ] Submit security artifacts for early review (Security Lead)

**Sprint Monitoring:**
- [ ] Daily dependency status check
- [ ] Mid-sprint design checkpoint
- [ ] Security review progress tracking
- [ ] Team velocity monitoring

**Contingency Plans:**
- **If email service delayed:** Implement basic registration without verification
- **If design approval blocked:** Use wireframes for basic functionality
- **If security review delayed:** Focus on non-security stories first

### 📊 Risk-Adjusted Capacity
- **Original Commitment:** 19 points
- **Risk-Adjusted Realistic:** 15 points
- **Minimum Viable Goal:** 12 points (core functionality)
```

### 💡 AI Planning Best Practices

**Data Quality:**
- Provide accurate team capacity information
- Include all constraints and dependencies
- Share historical velocity data
- Update with real-time changes

**Context Sharing:**
- Include business priorities and deadlines
- Share external dependencies and risks
- Provide team skills and availability
- Explain technical constraints

## Summary

AI-assisted planning transforms sprint planning from intuition-based to data-driven decision making. By analyzing capacity, dependencies, and risks systematically, teams can create more realistic commitments and proactively address potential issues.