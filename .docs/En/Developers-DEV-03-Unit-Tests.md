# Creating Unit Tests Automatically

**ID:** DEV-03  
**Platform:** GitHub Enterprise + Copilot  

## Target Audience
Developers

## AI Used
GitHub Enterprise

## AI Knowledge Level
Intermediate

## Technical Summary
Generate consistent unit tests from source code to avoid manual oversights and errors.

## Content

### 🧠 Introduction – AI for Code Quality

GitHub Copilot Enterprise revolutionizes unit test creation by automatically generating comprehensive test scenarios, including error cases that developers often forget. This approach allows you to:

- **Detect bugs** before they reach production
- **Cover all cases** including edge cases
- **Accelerate development** by automating test writing
- **Improve quality** through intelligent code analysis

### 🧪 Demonstration 1 — Creating a function with an error

#### 🎯 Goal
Intentionally create a Python function containing a logical error to demonstrate AI's ability to detect and correct problems.

#### ⚙️ Technical Steps

1. **Create a `calculator.py` file** with this function:

```python
def calculate_average(numbers):
    """
    Calculate the average of a list of numbers.
    
    Args:
        numbers (list): List of numbers
        
    Returns:
        float: The average of the numbers
    """
    if len(numbers) == 0:
        return 0
    
    total = sum(numbers)
    # INTENTIONAL ERROR: division by length + 1 instead of len(numbers)
    average = total / (len(numbers) + 1)
    return average

def divide_numbers(a, b):
    """
    Divide two numbers.
    
    Args:
        a (float): The dividend
        b (float): The divisor
        
    Returns:
        float: The result of the division
    """
    # INTENTIONAL ERROR: no check for division by zero
    return a / b
```

#### 💡 Key Points
- The `calculate_average` function has a **calculation error** (+ 1 in divisor)
- The `divide_numbers` function lacks **division by zero handling**
- These errors are **subtle** and common in development

### 🧪 Demonstration 2 — Generating unit tests with AI

#### 🎯 Goal
Use GitHub Copilot to automatically generate comprehensive unit tests that will reveal errors in our code.

#### ⚙️ Technical Steps

1. **Select the functions** in `calculator.py`

2. **Open Copilot Chat** and ask:
```
Generate comprehensive unit tests for these Python functions.
Include tests for normal cases, edge cases, and error cases.
Use pytest as the test framework.
```

3. **Copilot generates** the `test_calculator.py` file:

```python
import pytest
from calculator import calculate_average, divide_numbers

class TestCalculateAverage:
    
    def test_calculate_average_normal_case(self):
        """Test with a normal list of numbers"""
        numbers = [1, 2, 3, 4, 5]
        result = calculate_average(numbers)
        expected = 3.0  # (1+2+3+4+5) / 5 = 15/5 = 3.0
        assert result == expected, f"Expected {expected}, got {result}"
    
    def test_calculate_average_single_number(self):
        """Test with a single number"""
        numbers = [10]
        result = calculate_average(numbers)
        expected = 10.0
        assert result == expected, f"Expected {expected}, got {result}"
    
    def test_calculate_average_empty_list(self):
        """Test with empty list"""
        numbers = []
        result = calculate_average(numbers)
        expected = 0
        assert result == expected, f"Expected {expected}, got {result}"
    
    def test_calculate_average_negative_numbers(self):
        """Test with negative numbers"""
        numbers = [-2, -4, -6]
        result = calculate_average(numbers)
        expected = -4.0  # (-2-4-6) / 3 = -12/3 = -4.0
        assert result == expected, f"Expected {expected}, got {result}"

class TestDivideNumbers:
    
    def test_divide_normal_case(self):
        """Test normal division"""
        result = divide_numbers(10, 2)
        expected = 5.0
        assert result == expected, f"Expected {expected}, got {result}"
    
    def test_divide_decimal_result(self):
        """Test with decimal result"""
        result = divide_numbers(7, 3)
        expected = 7/3
        assert abs(result - expected) < 0.0001, f"Expected {expected}, got {result}"
    
    def test_divide_by_zero(self):
        """Test division by zero - should raise exception"""
        with pytest.raises(ZeroDivisionError):
            divide_numbers(10, 0)
    
    def test_divide_negative_numbers(self):
        """Test with negative numbers"""
        result = divide_numbers(-10, 2)
        expected = -5.0
        assert result == expected, f"Expected {expected}, got {result}"
```

#### 💡 Key Points
- Copilot **automatically generates** varied test cases
- It includes **error cases** like division by zero
- Tests are **well structured** with clear descriptions

### 🧪 Demonstration 3 — Running tests and identifying errors

#### 🎯 Goal
Execute the generated tests to reveal errors in our code and analyze results with AI assistance.

#### ⚙️ Technical Steps

1. **Install pytest** if needed:
```bash
pip install pytest
```

2. **Run the tests**:
```bash
pytest test_calculator.py -v
```

3. **Observe the failures**:
```
test_calculator.py::TestCalculateAverage::test_calculate_average_normal_case FAILED
test_calculator.py::TestCalculateAverage::test_calculate_average_single_number FAILED
test_calculator.py::TestCalculateAverage::test_calculate_average_negative_numbers FAILED
test_calculator.py::TestDivideNumbers::test_divide_by_zero FAILED

================================== FAILURES ==================================
______ TestCalculateAverage.test_calculate_average_normal_case ______

    def test_calculate_average_normal_case(self):
        numbers = [1, 2, 3, 4, 5]
        result = calculate_average(numbers)
        expected = 3.0  # (1+2+3+4+5) / 5 = 15/5 = 3.0
>       assert result == expected, f"Expected {expected}, got {result}"
E       AssertionError: Expected 3.0, got 2.5

______ TestDivideNumbers.test_divide_by_zero ______

    def test_divide_by_zero(self):
        with pytest.raises(ZeroDivisionError):
>           divide_numbers(10, 0)
E       ZeroDivisionError: division by zero
```

4. **Ask Copilot** to analyze the errors:
```
Analyze these failing test results.
What do they reveal about the errors in calculator.py?
```

#### 💡 Key Points
- Tests **immediately reveal** problems
- AI helps **interpret** failure results
- Error messages are **informative**

### 🧪 Demonstration 4 — Fixing errors with AI assistance

#### 🎯 Goal
Use Copilot to identify and fix errors detected by unit tests.

#### ⚙️ Technical Steps

1. **Show the failing code** to Copilot Chat:
```
Here is my calculate_average function that fails tests.
Tests expected 3.0 but received 2.5 for [1,2,3,4,5].
Identify and fix the error:

[paste the function code]
```

2. **Copilot identifies the error** and suggests the fix:
```python
def calculate_average(numbers):
    """
    Calculate the average of a list of numbers.
    
    Args:
        numbers (list): List of numbers
        
    Returns:
        float: The average of the numbers
    """
    if len(numbers) == 0:
        return 0
    
    total = sum(numbers)
    # FIX: division by len(numbers) instead of len(numbers) + 1
    average = total / len(numbers)
    return average
```

3. **For the divide_numbers function**, ask:
```
My divide_numbers function needs to handle division by zero.
How can I improve it?
```

4. **Copilot suggests**:
```python
def divide_numbers(a, b):
    """
    Divide two numbers.
    
    Args:
        a (float): The dividend
        b (float): The divisor
        
    Returns:
        float: The result of the division
        
    Raises:
        ZeroDivisionError: If divisor is zero
    """
    if b == 0:
        raise ZeroDivisionError("Cannot divide by zero")
    return a / b
```

#### 💡 Key Points
- Copilot **quickly identifies** logical errors
- It suggests **precise corrections**
- It also improves **function documentation**

### 🧪 Demonstration 5 — Final validation

#### 🎯 Goal
Verify that corrections are effective by re-running all tests.

#### ⚙️ Technical Steps

1. **Apply corrections** to the `calculator.py` file

2. **Re-run the tests**:
```bash
pytest test_calculator.py -v
```

3. **Observe success**:
```
test_calculator.py::TestCalculateAverage::test_calculate_average_normal_case PASSED
test_calculator.py::TestCalculateAverage::test_calculate_average_single_number PASSED
test_calculator.py::TestCalculateAverage::test_calculate_average_empty_list PASSED
test_calculator.py::TestCalculateAverage::test_calculate_average_negative_numbers PASSED
test_calculator.py::TestDivideNumbers::test_divide_normal_case PASSED
test_calculator.py::TestDivideNumbers::test_divide_decimal_result PASSED
test_calculator.py::TestDivideNumbers::test_divide_by_zero PASSED
test_calculator.py::TestDivideNumbers::test_divide_negative_numbers PASSED

======================== 8 passed in 0.03s ========================
```

4. **Request a coverage report**:
```bash
pytest --cov=calculator test_calculator.py
```

#### 💡 Key Points
- **100% success** after correction
- **Code coverage** is optimal
- The process is **fast and efficient**

## Summary

This article demonstrates the **complete AI-assisted development cycle** for creating and validating automated unit tests.

**5-step process:**
1. **🐛 Intentional creation** of a function with logical errors
2. **🤖 Automatic generation** of comprehensive unit tests by Copilot
3. **🔍 Execution and analysis** of test failures 
4. **🔧 Assisted correction** of errors identified by AI
5. **✅ Final validation** with all tests passing

**Demonstrated benefits:**
- **Automatic detection** of subtle errors (incorrect calculation, division by zero)
- **Exhaustive generation** of test cases (normal, edge, error cases)
- **Guided correction** with clear explanations of problems
- **Rapid cycle** of development-test-correction

**Result:** GitHub Copilot Enterprise transforms unit test creation from a chore into an intelligent collaborative process that significantly improves code quality.