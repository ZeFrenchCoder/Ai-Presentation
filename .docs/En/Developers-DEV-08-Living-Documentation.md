# Living Documentation with AI

**ID:** DEV-08  
**Platform:** ChatGPT + GitHub Wiki  

## Target Audience
Developers

## AI Used
ChatGPT/MS Copilot

## AI Knowledge Level
Advanced

## Technical Summary
AI creates and updates technical documentation from commits and code.

## Content

### 🧠 Introduction

**Technical documentation** is often outdated or incomplete. Developers write code but neglect documentation, creating maintenance and onboarding issues.

**AI can automate** documentation creation:
- **Document functions** directly in code
- **Explain tests** with ticket references
- **Generate complete system docs**
- **Create startup guides**

**Advantage**: Documentation always up-to-date and synchronized with code.

### 🧪 Example 1 — Documenting a function in code

#### Situation
You have a function in your .NET API and want to document it properly.

#### What you do

1. **Your function without docs**:
```csharp
// Controllers/UsersController.cs
public async Task<ActionResult<UserDto>> GetUserById(int id)
{
    var user = await _userService.GetUserByIdAsync(id);
    if (user == null)
        return NotFound($"User with ID {id} not found");
    
    return Ok(_mapper.Map<UserDto>(user));
}
```

2. **Ask Copilot**:
```
@workspace Document this C# function with:
- Summary of what it does
- Parameters and their validation
- Possible returns with HTTP codes
- Usage example

Standard .NET XML format
```

3. **Copilot generates the documentation**:
```csharp
// Controllers/UsersController.cs

/// <summary>
/// Retrieves a specific user by their unique identifier.
/// </summary>
/// <param name="id">The unique identifier of the user (must be positive)</param>
/// <returns>
/// User information in UserDto format if found,
/// otherwise returns NotFound (404)
/// </returns>
/// <response code="200">User found and returned successfully</response>
/// <response code="404">No user found with this ID</response>
/// <response code="400">Invalid ID (negative or zero)</response>
/// <example>
/// GET /api/users/123
/// Returns: { "id": 123, "name": "John Doe", "email": "john@example.com" }
/// </example>
/// <remarks>
/// This method uses the UserService to access data.
/// Mapping to UserDto excludes sensitive information like passwords.
/// </remarks>
[HttpGet("{id}")]
public async Task<ActionResult<UserDto>> GetUserById(int id)
{
    var user = await _userService.GetUserByIdAsync(id);
    if (user == null)
        return NotFound($"User with ID {id} not found");
    
    return Ok(_mapper.Map<UserDto>(user));
}
```

### 🧪 Example 2 — Documenting tests with ticket reference

#### Situation
You're writing unit tests for a Jira story and want to document the context.

#### What you do

1. **Your test without documentation**:
```csharp
// Tests/UsersControllerTests.cs
[Test]
public async Task GetUserById_ReturnsUser_WhenUserExists()
{
    var userId = 123;
    var user = new User { Id = userId, Name = "Test User" };
    _userService.Setup(x => x.GetUserByIdAsync(userId)).ReturnsAsync(user);

    var result = await _controller.GetUserById(userId);
    
    Assert.IsInstanceOf<OkObjectResult>(result.Result);
}
```

2. **Ask Copilot**:
```
@workspace Document this test with:
- Reference to Jira ticket US-456
- Business context of the test
- Tested scenario
- Validated acceptance criteria

Standard format with Given/When/Then
```

3. **Copilot documents the test**:
```csharp
// Tests/UsersControllerTests.cs

/// <summary>
/// User retrieval test - Success case
/// 
/// Ticket: US-456 - "As an admin, I want to view a user's profile 
/// to verify their personal information"
/// 
/// Business context: 
/// Administrators must be able to access user profiles for 
/// customer support and account management.
/// 
/// Scenario: Successful consultation of an existing user profile
/// 
/// Validated acceptance criteria:
/// - ✅ AC1: API returns user data when ID exists
/// - ✅ AC2: Response format respects UserDto contract
/// - ✅ AC3: HTTP return code is 200 OK
/// </summary>
/// <remarks>
/// Given: A user exists with ID 123 in the database
/// When: Admin makes a GET /api/users/123 request  
/// Then: API returns 200 OK with data in UserDto format
/// 
/// Reference: https://jira.company.com/browse/US-456
/// </remarks>
[Test]
public async Task GetUserById_ReturnsUser_WhenUserExists()
{
    // Arrange - Given: A user exists in the system
    var userId = 123;
    var user = new User { Id = userId, Name = "Test User", Email = "test@example.com" };
    _userService.Setup(x => x.GetUserByIdAsync(userId)).ReturnsAsync(user);

    // Act - When: Admin requests this user's info
    var result = await _controller.GetUserById(userId);
    
    // Assert - Then: API returns data successfully
    Assert.IsInstanceOf<OkObjectResult>(result.Result);
    var okResult = result.Result as OkObjectResult;
    var userDto = okResult.Value as UserDto;
    Assert.AreEqual(userId, userDto.Id);
    Assert.AreEqual("Test User", userDto.Name);
}
```

### 🧪 Example 3 — Documenting the complete system

#### Situation
You want to generate complete system documentation in `./docs/system.md`.

#### What you do

1. **Ask Copilot**:
```
@workspace Generate complete system documentation in ./docs/system.md for our .NET API

Include:
- General architecture
- Available APIs with examples
- Database and entities
- Services and dependencies
- Configuration and deployment

End with date, ticket US-789 and user andre.theriault@cgi.com
```

2. **Copilot generates** `./docs/system.md`:
```markdown
## System Documentation - UserManagement API

## 🏗️ General Architecture

This .NET Core 6.0 API provides a user management system with JWT authentication and SQL Server database.

```
┌─────────────────┐    ┌─────────────────┐    ┌─────────────────┐
│   Web Client    │────│   API Gateway   │────│  UserMgmt API   │
└─────────────────┘    └─────────────────┘    └─────────────────┘
                                                        │
                                               ┌─────────────────┐
                                               │  SQL Server DB  │
                                               └─────────────────┘
```

## 📡 Available APIs

### User Management
```http
GET    /api/users           # List all users
GET    /api/users/{id}      # Get user by ID
POST   /api/users           # Create new user
PUT    /api/users/{id}      # Update user
DELETE /api/users/{id}      # Delete user
```

### Authentication
```http
POST   /api/auth/login      # User login
POST   /api/auth/logout     # Logout
POST   /api/auth/refresh    # JWT token renewal
```

### Usage Example
```bash
## Create a user
curl -X POST https://api.company.com/api/users \
  -H "Content-Type: application/json" \
  -H "Authorization: Bearer {token}" \
  -d '{
    "name": "John Doe",
    "email": "john.doe@company.com",
    "role": "User"
  }'

## Response
{
  "id": 456,
  "name": "John Doe", 
  "email": "john.doe@company.com",
  "role": "User",
  "createdAt": "2025-10-13T10:30:00Z"
}
```

## 🗄️ Database

### User Entity
```sql
CREATE TABLE Users (
    Id int IDENTITY(1,1) PRIMARY KEY,
    Name nvarchar(100) NOT NULL,
    Email nvarchar(255) NOT NULL UNIQUE,
    PasswordHash nvarchar(255) NOT NULL,
    Role nvarchar(50) NOT NULL DEFAULT 'User',
    CreatedAt datetime2 NOT NULL DEFAULT GETDATE(),
    UpdatedAt datetime2 NOT NULL DEFAULT GETDATE(),
    IsActive bit NOT NULL DEFAULT 1
);
```

### Relations
- One user can have multiple sessions (UserSessions table)
- One user can have multiple roles (UserRoles table)

## 🔧 Services and Dependencies

### Main Services
- **UserService**: User business logic
- **AuthService**: JWT authentication management
- **EmailService**: Email notifications
- **AuditService**: Action traceability

### NuGet Dependencies
```xml
<PackageReference Include="Microsoft.AspNetCore.Authentication.JwtBearer" Version="6.0.0" />
<PackageReference Include="Microsoft.EntityFrameworkCore.SqlServer" Version="6.0.0" />
<PackageReference Include="AutoMapper" Version="12.0.0" />
<PackageReference Include="FluentValidation" Version="11.0.0" />
<PackageReference Include="Serilog" Version="2.12.0" />
```

## ⚙️ Configuration

### Environment Variables
```bash
# Database
ConnectionStrings__DefaultConnection=Server=localhost;Database=UserMgmtDB;Trusted_Connection=true;

# JWT
JwtSettings__Secret=your-super-secret-key-min-256-bits
JwtSettings__Issuer=UserMgmtAPI
JwtSettings__ExpiryInHours=24

# Email
EmailSettings__SmtpServer=smtp.company.com
EmailSettings__Port=587
EmailSettings__Username=noreply@company.com
EmailSettings__Password=smtp-password
```

### Deployment
```bash
## Build
dotnet build --configuration Release

## Tests
dotnet test

## Publish
dotnet publish --configuration Release --output ./publish

## Docker
docker build -t usermgmt-api .
docker run -p 8080:80 usermgmt-api
```

## 📊 Monitoring

### Health Endpoints
- `GET /health` - General API status
- `GET /health/db` - Database status
- `GET /health/ready` - API ready to receive traffic

### Logs
- **Serilog** configured with daily rotation
- Logs stored in `/logs/` and sent to Seq
- Levels: Debug, Info, Warning, Error, Fatal

## 🚀 Performance

### Target Metrics
- **Response time**: < 200ms (95th percentile)
- **Throughput**: > 1000 req/sec
- **Availability**: 99.9% SLA
- **Database**: < 50ms per query

---

*Documentation generated on October 13, 2025*  
*Ticket: US-789*  
*User: andre.theriault@cgi.com*


### 🧪 Example 4 — System startup guide

#### Situation
New developer joining the team who needs a guide to start the project.

#### What you do

1. **Ask Copilot**:
```
@workspace Create a startup guide in ./docs/getting-started.md

For a new dev who wants to:
- Clone and setup the project
- Install dependencies
- Configure the database
- Launch the application
- Run first tests

Clear steps with exact commands. End with date, ticket DEV-123 and user.
```

2. **Copilot creates** `./docs/getting-started.md`:
```markdown
## Getting Started Guide - UserManagement API

## 🚀 Initial Setup

### Prerequisites
- .NET 6.0 SDK or newer
- SQL Server (LocalDB sufficient for development)
- Visual Studio 2022 or VS Code
- Git

### Prerequisites Check
```bash
## Check .NET
dotnet --version
## Should display 6.0.x or newer

## Check SQL Server LocalDB
sqllocaldb info
## Should list available instances


## 📥 Clone Project

## Clone repository
git clone https://github.com/company/usermanagement-api.git
cd usermanagement-api

## Create your development branch
git checkout -b feature/your-name-setup

## Restore dependencies
dotnet restore

...
...
...
```
## Summary

**Living Documentation with AI** transforms documentation maintenance by automating:

### ✅ Practical Benefits
- **Synchronized documentation** with code in real-time
- **Standards respected** (XML .NET, ticket references, concrete examples)
- **Complete guides** generated automatically
- **Traceability** with dates, tickets and users

### 🎯 Types of automated documentation
1. **Functions**: XML documentation in code with examples
2. **Tests**: Business context with Jira/DevOps references
3. **System**: Complete architecture with APIs and deployment
4. **Guides**: Step-by-step procedures for new developers

### 🚀 In practice
- **Self-documented code** with business context
- **Explicit tests** linked to user stories
- **Up-to-date architecture** with usage examples
- **Simplified onboarding** with detailed guides

AI maintains **living** documentation that evolves with the code, eliminating the traditional gap between code and documentation.
