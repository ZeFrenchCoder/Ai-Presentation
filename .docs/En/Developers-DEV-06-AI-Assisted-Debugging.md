# AI-Assisted Debugging: Understanding Errors Faster

**ID:** DEV-06  
**Platform:** ChatGPT + IDE Integration  

## Target Audience
Developers

## AI Used
ChatGPT/MS Copilot

## AI Knowledge Level
Beginner

## Technical Summary
Describe your error, AI proposes hypotheses, explanations and testable solutions.

## Content

### 🧠 Introduction – AI-Assisted Debugging

**AI-Assisted Debugging** revolutionizes error resolution by transforming the traditional debugging process. Instead of spending hours searching for the cause of a bug, you collaborate with an AI that:

- **Automatically analyzes** error messages and context
- **Proposes hypotheses** based on millions of similar cases
- **Suggests solutions** step by step and testable
- **Explains root causes** to prevent recurrence
- **Guides the process** of resolution methodically

This approach allows for **drastically reducing** debugging time while **improving understanding** of encountered errors.

### 🧪 Demonstration 1 — Error analysis with complete context

#### 🎯 Goal
Learn to effectively present an error to AI to get accurate analysis and targeted solutions.

#### ⚙️ Technical Steps

1. **Prepare complete error context**:
```python
# Code that generates the error
def process_user_data(data_file):
    with open(data_file, 'r') as f:
        users = json.loads(f.read())
    
    results = []
    for user in users:
        age = datetime.now().year - user['birth_year']
        if age >= 18:
            results.append({
                'name': user['name'],
                'age': age,
                'status': 'adult'
            })
    return results

# Error occurred:
# TypeError: unsupported operand type(s) for -: 'int' and 'str'
```

2. **Present to AI with structured format**:
```
I have a Python error I need help debugging:

ERROR MESSAGE:
TypeError: unsupported operand type(s) for -: 'int' and 'str'

CODE CONTEXT:
[paste the function above]

ENVIRONMENT:
- Python 3.9
- Processing JSON user data
- Error occurs on line: age = datetime.now().year - user['birth_year']

WHAT I TRIED:
- Checked file exists and contains data
- Verified JSON structure looks correct

Please analyze this error and suggest solutions.
```

3. **AI provides systematic analysis**:
```markdown
🔍 ERROR ANALYSIS:

**Root Cause:**
The error occurs because `user['birth_year']` is a string type (from JSON), but you're trying to subtract it from an integer (`datetime.now().year`).

**Why this happens:**
JSON doesn't have separate integer/string types - numbers can be stored as strings.

**Solutions (in order of preference):**

1. **Type conversion (quick fix):**
```python
age = datetime.now().year - int(user['birth_year'])
```

2. **Defensive programming (recommended):**
```python
try:
    birth_year = int(user['birth_year'])
    age = datetime.now().year - birth_year
except ValueError:
    print(f"Invalid birth_year for user {user.get('name', 'unknown')}")
    continue
```

3. **Data validation (best practice):**
```python
def validate_user_data(user):
    required_fields = ['name', 'birth_year']
    for field in required_fields:
        if field not in user:
            raise ValueError(f"Missing required field: {field}")
    
    try:
        birth_year = int(user['birth_year'])
        if birth_year < 1900 or birth_year > datetime.now().year:
            raise ValueError(f"Invalid birth_year: {birth_year}")
    except ValueError:
        raise ValueError(f"birth_year must be a valid integer")
    
    return True
```
```

#### 💡 Key Points
- AI **identifies the exact type mismatch** issue
- Provides **multiple solution levels** from quick fix to best practice
- **Explains the underlying cause** for learning

### 🧪 Demonstration 2 — Stack trace analysis

#### 🎯 Goal
Use AI to decode complex stack traces and identify the actual problem source.

#### ⚙️ Technical Steps

1. **Present complex error with full stack trace**:
```
I'm getting this error in my web application:

FULL STACK TRACE:
Traceback (most recent call last):
  File "/app/main.py", line 45, in process_request
    result = calculate_metrics(user_data)
  File "/app/analytics.py", line 23, in calculate_metrics
    score = compute_user_score(data['activities'])
  File "/app/analytics.py", line 67, in compute_user_score
    weighted_score = sum(activity['weight'] * activity['points'] for activity in activities)
  File "/app/analytics.py", line 67, in <genexpr>
    weighted_score = sum(activity['weight'] * activity['points'] for activity in activities)
KeyError: 'weight'

CONTEXT:
- Web API processing user analytics
- Error happens randomly, not for all users
- Started happening after recent data migration

What's the issue and how do I fix it?
```

2. **AI provides comprehensive analysis**:
```markdown
🎯 STACK TRACE ANALYSIS:

**Error Location:**
Line 67 in analytics.py - the issue is in the generator expression inside `sum()`

**Problem:**
Some activity objects don't have a 'weight' key, causing KeyError when the generator tries to access it.

**Why it's random:**
- Only affects users whose activities data is missing the 'weight' field
- Likely caused by data migration not handling all edge cases

**Immediate Fix:**
```python
# Before (problematic):
weighted_score = sum(activity['weight'] * activity['points'] for activity in activities)

# After (defensive):
weighted_score = sum(
    activity.get('weight', 1.0) * activity.get('points', 0) 
    for activity in activities
)
```

**Better Solution:**
```python
def compute_user_score(activities):
    total_score = 0
    for activity in activities:
        weight = activity.get('weight')
        points = activity.get('points')
        
        if weight is None:
            logging.warning(f"Missing weight for activity: {activity.get('id', 'unknown')}")
            weight = 1.0  # default value
            
        if points is None:
            logging.warning(f"Missing points for activity: {activity.get('id', 'unknown')}")
            points = 0
            
        total_score += weight * points
    
    return total_score
```

**Data Migration Fix:**
```sql
-- Check for missing weights
SELECT id, activity_type FROM activities WHERE weight IS NULL;

-- Fix missing weights with defaults
UPDATE activities 
SET weight = 1.0 
WHERE weight IS NULL;
```


#### 💡 Key Points
- AI **traces the exact error path** through the stack
- **Identifies why it's intermittent** (data inconsistency)
- Provides **immediate fix + long-term solution**
- Includes **data investigation queries**

### 📊 Debug Workflow with AI

#### Standard debugging process:
1. **Error Collection**: Gather complete error information
2. **Context Presentation**: Structure the problem for AI analysis
3. **Hypothesis Generation**: AI suggests possible causes
4. **Solution Testing**: Implement and validate fixes
5. **Learning Integration**: Understand root causes

#### Template for AI debugging:
```
DEBUGGING REQUEST:

ERROR:
[Exact error message]

CODE:
[Relevant code section]

ENVIRONMENT:
[Language version, dependencies, OS]

CONTEXT:
[What the code should do, when error occurs]

ATTEMPTED FIXES:
[What you already tried]

REQUEST:
Please analyze and provide step-by-step solution.
```

## Summary

**AI-Assisted Debugging** transforms error resolution from a frustrating trial-and-error process into a systematic, educational experience.

**Key Benefits:**
- **Faster resolution**: AI immediately identifies common error patterns
- **Better understanding**: Explanations help prevent similar issues
- **Multiple solutions**: From quick fixes to best practices
- **Learning acceleration**: Turn debugging into teaching moments

**Best Practices:**
- **Provide complete context**: Error message, code, environment
- **Structure requests clearly**: Use consistent format for AI analysis
- **Test suggestions systematically**: Validate each proposed solution
- **Learn from patterns**: Build understanding of common error types

This approach doesn't replace debugging skills but **amplifies them**, making developers more effective at identifying and resolving issues while continuously improving their understanding of code behavior.