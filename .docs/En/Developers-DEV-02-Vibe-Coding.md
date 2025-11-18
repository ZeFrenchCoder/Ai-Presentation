# Vibe Coding: Coding in Collaboration with AI

**ID:** DEV-02  
**Platform:** GitHub Enterprise + Vibe Coding  

## Target Audience
Developers

## AI Used
GitHub Enterprise

## AI Knowledge Level
Intermediate

## Technical Summary
Using GitHub Copilot as a code partner to accelerate development and improve readability.

## Content

### 🧠 Introduction – Vibe Coding with GitHub Enterprise

**Vibe Coding** transforms your way of coding by creating a continuous dialogue with GitHub Copilot Enterprise. Instead of coding directly, you describe your intentions in working files, then collaborate with AI to execute your ideas step by step.

This approach allows you to:
- **Clarify your objectives** before starting
- **Decompose complex tasks** automatically
- **Validate your work** with AI assistance
- **Maintain a trace** of your development process

### 🧪 Demonstration 1 — Creating a planning file (todo.txt)

#### 🎯 Goal
Learn to clearly express your development intentions in a format that Copilot Enterprise can analyze and decompose.

#### ⚙️ Technical Steps

1. **Create a `todo.txt` file** in your project

2. **Describe your main objective** in natural language:
```markdown
# Objective: Create a REST API to manage users

## Desired features:
- GET /users endpoint to list all users
- POST /users endpoint to create a new user
- PUT /users/{id} endpoint to modify an existing user
- DELETE /users/{id} endpoint to delete a user
- Input data validation
- Appropriate error handling
- Unit tests for each endpoint

## Technical constraints:
- Use Node.js with Express
- MongoDB database
- JWT authentication
- OpenAPI documentation
```

#### 💡 Key Points
- Be **specific** about expected features
- Include **technical constraints** from the start
- Think about **quality aspects** (tests, error handling)

### 🧪 Demonstration 2 — Analyzing with Copilot Enterprise (TodoAI.md)

#### 🎯 Goal
Use Copilot Enterprise to analyze your todo.txt file and generate a structured execution plan.

#### ⚙️ Technical Steps

1. **Open Copilot Chat** in VS Code

2. **Select the content** of your `todo.txt` file

3. **Ask Copilot** to analyze and create a plan:
```
Analyze the content of todo.txt and create a TodoAI.md file with:
- A step-by-step plan
- Title, status and summary for each task
- Recommended execution order
- Time estimation for each step
```

4. **Copilot generates** a structured `TodoAI.md` file:
```markdown
# Execution Plan - Users API

## Step 1: Project setup
**Status:** 🔄 To do  
**Summary:** Initialize Node.js project with necessary dependencies  
**Estimated time:** 30 minutes

### Detailed tasks:
- npm init -y
- Install Express, MongoDB, JWT, Jest
- Configure folder structure

## Step 2: User model
**Status:** 🔄 To do  
**Summary:** Create MongoDB schema for users  
**Estimated time:** 45 minutes

### Detailed tasks:
- Define user schema (name, email, password)
- Field validation
- Password hashing methods

## Step 3: CRUD endpoints
**Status:** 🔄 To do  
**Summary:** Implement the 4 main endpoints  
**Estimated time:** 2 hours

### Detailed tasks:
- GET /users (with pagination)
- POST /users (with validation)
- PUT /users/{id}
- DELETE /users/{id}
```

#### 💡 Key Points
- Copilot **automatically decomposes** complex tasks
- It suggests a **logical order** of execution
- **Time estimates** help with planning

### 🧪 Demonstration 3 — Step-by-step execution

#### 🎯 Goal
Collaborate with Copilot to execute each step of the plan by requesting specific code.

#### ⚙️ Technical Steps

1. **For each step** in TodoAI.md, use Copilot Chat:

```
Execute Step 1 from TodoAI.md: 
Generate the commands and code needed to configure the Node.js project
```

2. **Copilot responds** with concrete code:
```bash
# Commands to execute
npm init -y
npm install express mongoose bcryptjs jsonwebtoken jest supertest
npm install -D nodemon

# Folder structure
mkdir src controllers models routes middleware tests
```

3. **Request code** for each component:
```
Generate the server.js file for Step 1
```

4. **Mark the step as completed** in TodoAI.md:
```markdown
## Step 1: Project setup
**Status:** ✅ Completed  
**Actual time:** 25 minutes
```

#### 💡 Key Points
- **One step at a time** to maintain quality
- **Constant dialogue** with Copilot to adjust
- **Status updates** to track progress

### 🧪 Demonstration 4 — AI-assisted validation (validation.md)

#### 🎯 Goal
Create an AI-assisted validation process to verify the quality of completed work.

#### ⚙️ Technical Steps

1. **Ask Copilot** to create a validation plan:
```
Create a validation.md file to validate that the API meets:
- Original todo.txt requirements
- Security best practices
- Code quality
- Test coverage
```

2. **Copilot generates** a `validation.md` file:
```markdown
# Users API Validation

## ✅ Functional requirements checklist
- [ ] GET /users returns list of users
- [ ] POST /users creates a new user
- [ ] PUT /users/{id} modifies a user
- [ ] DELETE /users/{id} deletes a user
- [ ] Input data validation
- [ ] Appropriate error handling

## 🔒 Security checklist
- [ ] Passwords hashed with bcrypt
- [ ] Functional JWT authentication
- [ ] User input validation
- [ ] Protection against injections

## 🧪 Testing checklist
- [ ] Unit tests for each endpoint
- [ ] Coverage > 80%
- [ ] Integration tests
- [ ] Error validation tests

## 📋 Code quality checklist
- [ ] Commented and readable code
- [ ] Consistent folder structure
- [ ] Centralized error handling
- [ ] API documentation (OpenAPI)
```

3. **Execute validation** step by step with Copilot:
```
Help me verify the first point: test the GET /users endpoint
Generate a complete unit test
```

#### 💡 Key Points
- **Automated validation** ensures quality
- Copilot helps **identify gaps**
- The process is **reproducible** for other projects

## Summary

**Vibe Coding** revolutionizes development by creating a collaborative workflow between the developer and GitHub Copilot Enterprise.

**4-step process:**
1. **📝 Planning**: Expressing objectives in `todo.txt` 
2. **🤖 Analysis**: Automatic generation of detailed plan in `TodoAI.md`
3. **⚡ Execution**: Step-by-step development with Copilot assistance
4. **✅ Validation**: Quality verification via `validation.md`

**Key benefits:**
- **Clear objectives** before starting to code
- **Automatic decomposition** of complex tasks
- **Complete traceability** of the development process
- **Guaranteed quality** through assisted validation

**Result:** A more structured, collaborative and qualitative development method that transforms Copilot into a true code partner.