# Creating Unit Tests Automatically (QA Version)

**ID:** QA-02  
**Platform:** GitHub Enterprise + Copilot  

## Target Audience
QA / Testers

## AI Used
GitHub Enterprise

## AI Knowledge Level
Beginner

## Technical Summary
Create or validate consistent unit tests with functional specifications and generate detailed manual test cases.

## Content

### Demonstration: Code Analysis and Manual Test Case Generation

#### Step 1: Analyze Source Code

Let's assume we have a price calculation function with discount:

```javascript
function calculatePrice(basePrice, discountPercent, customerType, quantity) {
    // Parameter validation
    if (basePrice <= 0) {
        throw new Error("Base price must be positive");
    }
    
    if (discountPercent < 0 || discountPercent > 100) {
        throw new Error("Discount percentage must be between 0 and 100");
    }
    
    if (quantity <= 0) {
        throw new Error("Quantity must be positive");
    }
    
    // Price calculation with discount
    let discountAmount = (basePrice * discountPercent) / 100;
    let discountedPrice = basePrice - discountAmount;
    
    // Additional discount based on customer type
    if (customerType === "VIP") {
        discountedPrice *= 0.95; // 5% additional discount
    } else if (customerType === "PREMIUM") {
        discountedPrice *= 0.97; // 3% additional discount
    }
    
    // Total calculation
    return discountedPrice * quantity;
}
```

#### Step 2: Ask AI to Generate Test Cases

**Prompt to Copilot:**
```
Analyze this price calculation function and generate comprehensive test cases for QA testing.

Include:
1. Happy path scenarios
2. Edge cases
3. Error scenarios
4. Boundary value testing
5. Equivalence class testing

Format as detailed test cases with:
- Test ID
- Description
- Test steps
- Expected results
- Priority (High/Medium/Low)
```

#### Step 3: AI-Generated Test Cases

**AI Response:**
```markdown
## Test Cases for calculatePrice Function

## TC-001: Valid Price Calculation (Happy Path)
**Priority:** High
**Description:** Verify price calculation with valid inputs
**Test Steps:**
1. Call calculatePrice(100, 10, "STANDARD", 2)
2. Verify return value
**Expected Result:** 180 (100 - 10% = 90, × 2 = 180)

## TC-002: VIP Customer Discount
**Priority:** High  
**Description:** Verify additional 5% discount for VIP customers
**Test Steps:**
1. Call calculatePrice(100, 10, "VIP", 1)
2. Verify return value
**Expected Result:** 85.5 (100 - 10% = 90, - 5% = 85.5)

## TC-003: Premium Customer Discount
**Priority:** High
**Description:** Verify additional 3% discount for Premium customers  
**Test Steps:**
1. Call calculatePrice(100, 10, "PREMIUM", 1)
2. Verify return value
**Expected Result:** 87.3 (100 - 10% = 90, - 3% = 87.3)

## TC-004: Zero Discount
**Priority:** Medium
**Description:** Verify calculation with no discount
**Test Steps:**
1. Call calculatePrice(100, 0, "STANDARD", 1)
2. Verify return value
**Expected Result:** 100

## TC-005: Maximum Discount
**Priority:** Medium
**Description:** Verify calculation with 100% discount
**Test Steps:**
1. Call calculatePrice(100, 100, "STANDARD", 1)
2. Verify return value
**Expected Result:** 0

## TC-006: Invalid Base Price (Negative)
**Priority:** High
**Description:** Verify error handling for negative base price
**Test Steps:**
1. Call calculatePrice(-10, 10, "STANDARD", 1)
2. Verify error is thrown
**Expected Result:** Error: "Base price must be positive"

## TC-007: Invalid Discount (Negative)
**Priority:** High
**Description:** Verify error handling for negative discount
**Test Steps:**
1. Call calculatePrice(100, -5, "STANDARD", 1)
2. Verify error is thrown
**Expected Result:** Error: "Discount percentage must be between 0 and 100"

## TC-008: Invalid Discount (Over 100%)
**Priority:** High
**Description:** Verify error handling for discount over 100%
**Test Steps:**
1. Call calculatePrice(100, 150, "STANDARD", 1)
2. Verify error is thrown
**Expected Result:** Error: "Discount percentage must be between 0 and 100"

## TC-009: Invalid Quantity (Zero)
**Priority:** High
**Description:** Verify error handling for zero quantity
**Test Steps:**
1. Call calculatePrice(100, 10, "STANDARD", 0)
2. Verify error is thrown
**Expected Result:** Error: "Quantity must be positive"

## TC-010: Invalid Quantity (Negative)
**Priority:** High
**Description:** Verify error handling for negative quantity
**Test Steps:**
1. Call calculatePrice(100, 10, "STANDARD", -1)
2. Verify error is thrown
**Expected Result:** Error: "Quantity must be positive"

## TC-011: Boundary Value - Minimum Discount
**Priority:** Medium
**Description:** Test minimum boundary value for discount
**Test Steps:**
1. Call calculatePrice(100, 0.01, "STANDARD", 1)
2. Verify return value
**Expected Result:** 99.99

## TC-012: Boundary Value - Maximum Discount
**Priority:** Medium
**Description:** Test maximum boundary value for discount
**Test Steps:**
1. Call calculatePrice(100, 99.99, "STANDARD", 1)
2. Verify return value
**Expected Result:** 0.01

## TC-013: Unknown Customer Type
**Priority:** Medium
**Description:** Verify behavior with unknown customer type
**Test Steps:**
1. Call calculatePrice(100, 10, "UNKNOWN", 1)
2. Verify return value
**Expected Result:** 90 (no additional discount applied)
```

### Benefits for QA Teams

**Comprehensive Coverage:**
- AI generates test cases you might have missed
- Covers edge cases systematically
- Includes boundary value analysis

**Time Savings:**
- Reduces manual test case creation time by 70%
- Provides structured test format
- Includes expected results calculation

**Quality Improvement:**
- Ensures consistent test case format
- Reduces human error in test design
- Provides complete scenario coverage

### Best Practices for QA with AI

1. **Always review AI-generated tests** for business logic accuracy
2. **Add domain-specific test cases** that AI might miss
3. **Validate expected results** with business requirements
4. **Customize test format** to match your team's standards
5. **Use AI for regression test maintenance** when code changes

## Summary

AI-assisted test case generation transforms QA workflow by providing comprehensive, structured test cases quickly and consistently. This allows QA teams to focus on complex scenarios and business logic validation rather than repetitive test case creation.