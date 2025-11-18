# Creating Workflows or Creation Assistants

**ID:** DEV-09  
**Platform:** GitHub Enterprise + Custom Workflows  

## Target Audience
Developers

## AI Used
GitHub Enterprise

## AI Knowledge Level
Advanced

## Technical Summary
Create custom workflows and creation assistants to automate repetitive tasks and standardize development processes with GitHub Copilot Enterprise.

## Content

### 🧠 Introduction

Developers often do the **same repetitive tasks**: creating classes, controllers, tests, etc. Instead of asking the AI the same questions every time, you can create **assisted workflows** with JSON files.

**The idea**: The AI uses a configuration file to ask you the right questions in the right order and generate exactly what you need.

**Advantages**:
- **Standardization**: Same process for the whole team
- **Speed**: The AI knows what to ask  
- **Quality**: Nothing is forgotten
- **Reusability**: One workflow for multiple projects

### 🛠️ How it works

1. **You create** a JSON configuration file in `./workflows/`
2. **The AI reads** the workflow and follows the steps
3. **The AI asks** each question one by one
4. **The AI generates** the final code with your answers

### 🧪 Example 1 — Class creation workflow

#### Initial request: Create the workflow

**User** asks the AI:
> "I want to create a JSON configuration file for a workflow assistant that helps me create classes.
> 
> The workflow should ask me these questions:
> 1. What is the class name?
> 2. What are the class properties?
> 3. Any validations on the class?
> 4. Any calculations on the class?
> 5. Any special actions?
> 6. What output format (C#, VB.NET, Python, Java, Documentation)?
> 
> Create the file `./workflows/create-class-workflow.json` with all the necessary structure."

#### Step 1: AI creates the workflow file

AI generates `./workflows/create-class-workflow.json`:

```json
{
  "name": "Class Creator",
  "description": "Assistant to create a class with properties, validations and methods",
  "version": "1.0",
  "steps": [
    {
      "id": "class_name",
      "question": "What is the class name?",
      "type": "string",
      "required": true,
      "validation": "^[A-Z][a-zA-Z0-9]*$",
      "example": "Client, Product, Order"
    },
    {
      "id": "properties",
      "question": "What is the list of properties? (Format: name:type:description)",
      "type": "array",
      "required": true,
      "example": [
        "Id:int:Unique identifier",
        "Name:string:Client full name", 
        "Email:string:Email address",
        "DateCreated:DateTime:Creation date"
      ]
    },
    {
      "id": "validations",
      "question": "Any validations on the class? (Format: property:rule:message)",
      "type": "array",
      "required": false,
      "example": [
        "Name:Required:Name is required",
        "Email:EmailAddress:Invalid email format",
        "Id:Range(1,int.MaxValue):ID must be positive"
      ]
    },
    {
      "id": "calculations",
      "question": "Any calculations on the class? (Format: name:formula:description)",
      "type": "array", 
      "required": false,
      "example": [
        "Age:DateTime.Now.Year - DateOfBirth.Year:Calculate age",
        "IsActive:LastLoginDate > DateTime.Now.AddDays(-30):Client active if recent login"
      ]
    },
    {
      "id": "special_actions",
      "question": "Any special actions? (custom methods)",
      "type": "array",
      "required": false,
      "example": [
        "SendWelcomeEmail():Send welcome email",
        "GenerateReport():Generate client report",
        "UpdateLastActivity():Update last activity"
      ]
    },
    {
      "id": "output_format",
      "question": "What is the output format?",
      "type": "choice",
      "required": true,
      "options": ["C#", "VB.NET", "Python", "Java", "Documentation"],
      "default": "C#"
    }
  ],
  "output": {
    "template": "class_template.txt",
    "file_extension": {
      "C#": ".cs",
      "VB.NET": ".vb", 
      "Python": ".py",
      "Java": ".java",
      "Documentation": ".md"
    }
  }
}
```

#### Step 2: User makes their request

**User**: 
> "I want to create a Client Class."

#### Step 3: AI activates the workflow

**AI** reads the `./workflows/create-class-workflow.json` file and responds:

> I detected that you want to create a class. I'll use my assisted workflow to help you. 
> 
> **Question 1/6**: What is the class name?  
> *(Example: Client, Product, Order)*

**User**: `Client`

**AI**:
> Perfect! **Client** is a valid name.
>
> **Question 2/6**: What is the list of properties? (Format: name:type:description)  
> *(Example: Id:int:Unique identifier, Name:string:Full name)*

**User**: 
```
Id:int:Unique identifier
Name:string:Client full name
Email:string:Email address
Phone:string:Phone number
DateCreated:DateTime:Account creation date
IsActive:bool:Indicates if client is active
```

**AI**:
> Excellent! 6 properties recorded.
>
> **Question 3/6**: Any validations on the class? (Format: property:rule:message)  
> *(Optional - press Enter to skip)*

**User**:
```
Name:Required:Name is required
Email:EmailAddress:Invalid email format
Email:Required:Email is required
Phone:Phone:Invalid phone format
Id:Range(1,int.MaxValue):ID must be positive
```

**AI**:
> 5 validations added.
>
> **Question 4/6**: Any calculations on the class? (Format: name:formula:description)  
> *(Optional - press Enter to skip)*

**User**:
```
AccountAge:DateTime.Now.Subtract(DateCreated).Days:Account age in days
IsRecentClient:DateCreated > DateTime.Now.AddMonths(-3):Recent client (less than 3 months)
```

>
> **Question 5/6**: Any special actions? (custom methods)  
> *(Optional - press Enter to skip)*

**User**:
```
SendWelcomeEmail():Send welcome email to client
DeactivateAccount():Deactivate client account
GetOrderHistory():Retrieve order history
UpdateContactInfo(email, phone):Update contact info
```

**AI**:
> 4 special actions added.
>
> **Question 6/6**: What is the output format?  
> **Choices**: C# | VB.NET | Python | Java | Documentation

**User**: `C#`

#### Step 4: AI generates the code

**AI**:
> Perfect! I'm generating your **Client** class in C# with all specifications...

```csharp
using System;
using System.ComponentModel.DataAnnotations;
using System.Linq;

namespace YourProject.Models
{
    /// <summary>
    /// Represents a system client with personal information and associated methods
    /// Generated automatically on October 13, 2025
    /// </summary>
    public class Client
    {
        // Base properties
        
        /// <summary>
        /// Unique identifier
        /// </summary>
        [Required]
        [Range(1, int.MaxValue, ErrorMessage = "ID must be positive")]
        public int Id { get; set; }
        
        /// <summary>
        /// Client full name
        /// </summary>
        [Required(ErrorMessage = "Name is required")]
        public string Name { get; set; }
        
        /// <summary>
        /// Email address
        /// </summary>
        [Required(ErrorMessage = "Email is required")]
        [EmailAddress(ErrorMessage = "Invalid email format")]
        public string Email { get; set; }
        
        /// <summary>
        /// Phone number
        /// </summary>
        [Phone(ErrorMessage = "Invalid phone format")]
        public string Phone { get; set; }
        
        /// <summary>
        /// Account creation date
        /// </summary>
        public DateTime DateCreated { get; set; }
        
        /// <summary>
        /// Indicates if client is active
        /// </summary>
        public bool IsActive { get; set; }
        
        // Calculated properties
        
        /// <summary>
        /// Account age in days
        /// </summary>
        public int AccountAge => DateTime.Now.Subtract(DateCreated).Days;
        
        /// <summary>
        /// Recent client (less than 3 months)
        /// </summary>
        public bool IsRecentClient => DateCreated > DateTime.Now.AddMonths(-3);
        
        // Constructor
        
        public Client()
        {
            DateCreated = DateTime.Now;
            IsActive = true;
        }
        
        // Special actions
        
        /// <summary>
        /// Send welcome email to client
        /// </summary>
        public void SendWelcomeEmail()
        {
            // TODO: Implement welcome email sending
            Console.WriteLine($"Welcome email sent to {Email}");
        }
        
        /// <summary>
        /// Deactivate client account
        /// </summary>
        public void DeactivateAccount()
        {
            IsActive = false;
            Console.WriteLine($"Account {Name} deactivated");
        }
        
        /// <summary>
        /// Retrieve order history
        /// </summary>
        /// <returns>List of client orders</returns>
        public List<Order> GetOrderHistory()
        {
            // TODO: Implement order retrieval
            return new List<Order>();
        }
        
        /// <summary>
        /// Update contact information
        /// </summary>
        /// <param name="email">New email address</param>
        /// <param name="phone">New phone number</param>
        public void UpdateContactInfo(string email, string phone)
        {
            Email = email;
            Phone = phone;
            Console.WriteLine($"Contact information updated for {Name}");
        }
        
        public override string ToString()
        {
            return $"Client: {Name} ({Email}) - Created on {DateCreated:MM/dd/yyyy} - {(IsActive ? "Active" : "Inactive")}";
        }
    }
}
```

> **✅ Client class generated!**
>
> 📁 File saved: `./Models/Client.cs`  
> 🎯 Format: C# with DataAnnotations validations  
> 📊 Content: 6 properties, 5 validations, 2 calculations, 4 methods  
> ⏰ Generated on October 13, 2025

### 💡 Other workflow examples

You can create other workflows in `./workflows/`:

- `create-controller-workflow.json` - For API controllers
- `create-test-workflow.json` - For unit tests  
- `create-migration-workflow.json` - For database migrations
- `create-service-workflow.json` - For business services
- `create-dto-workflow.json` - For transfer objects
- It's also possible to ask questions one at a time.
- You can also ask AI to write standard steps for project creation, feature development, bugfix, Jira or DevOps ticket.

### 🎯 Workflow advantages

**For developers**:
- ✅ **No more omissions** - AI follows a checklist
- ✅ **Standardized code** - Same structure for everyone
- ✅ **Time savings** - No need to re-explain each time
- ✅ **Relevant questions** - AI knows what to ask

**For the team**:
- ✅ **Uniform process** - Same workflow for all devs
- ✅ **Knowledge sharing** - Workflows are shared
- ✅ **Continuous improvement** - Workflows evolve
- ✅ **Easier onboarding** - New devs follow the process

## Summary

**Workflow Assistants** allow creating guided processes where AI:

### ✅ What it brings
- **Standardizes** code creation with JSON configuration files
- **Guides the user** with structured questions one by one  
- **Automatically generates** code with all specifications
- **Avoids omissions** by following a complete checklist

### 🎯 In practice  
1. **Create** JSON workflows in `./workflows/`
2. **Use** structured questions with validation
3. **Let AI** guide the process step by step
4. **Get** standardized and complete code

### 🚀 Result
- **Consistent code** across the team
- **Repeatable processes** that can be improved
- **Significant time savings**
- **Quality guaranteed** by structure