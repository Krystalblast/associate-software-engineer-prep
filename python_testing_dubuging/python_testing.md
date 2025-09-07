# 🧪 Python Testing Notes

## 1. Why Test?
- Ensure code works correctly
- Prevent bugs when adding new features
- Enable safe refactoring
- Increase confidence in deployment

---

## 2. Types of Testing
- **Manual Testing** → run code, check output manually
- **Automated Testing** → use tools/frameworks to verify results
- **Unit Testing** → test small pieces (functions, methods)
- **Integration Testing** → test multiple modules together
- **Functional / End-to-End Testing** → simulate user interaction

---

## 3. Unit Testing with `unittest`
```python
import unittest

def add(a, b):
    return a + b

class TestMath(unittest.TestCase):
    def test_add(self):
        self.assertEqual(add(2, 3), 5)
        self.assertNotEqual(add(2, 2), 5)

if __name__ == "__main__":
    unittest.main()
```

🔑 Common assertions:
- `assertEqual`, `assertTrue`, `assertFalse`, `assertRaises`

---

## 4. Testing with `pytest`
```python
# test_math.py
def add(a, b):
    return a + b

def test_add():
    assert add(2, 3) == 5
    assert add(-1, 1) == 0
```

✨ Features:
- Simple function-based tests
- Fixtures for setup/teardown
- Plugins for extended functionality
- Clearer test reports

---

## 5. Doctest
```python
def multiply(a, b):
    """
    >>> multiply(2, 3)
    6
    >>> multiply(3, 0)
    0
    """
    return a * b

if __name__ == "__main__":
    import doctest
    doctest.testmod()
```
Use examples in docstrings as tests.

---

## 6. Organizing Tests
- Keep tests in a separate `tests/` folder
- File naming: `test_*.py`
- Tests should be repeatable & independent
- Cover edge cases
- Integrate with CI (e.g., GitHub Actions)

---

## 7. Coverage
```bash
pip install coverage
coverage run -m pytest
coverage report
```
- Measures % of code executed during tests
- Aim for high coverage, but focus on test quality too

---

## 8. Test-Driven Development (TDD)
Cycle: **Red → Green → Refactor**
1. Write a failing test (Red)
2. Write code to make it pass (Green)
3. Refactor while keeping tests passing

---

## 9. Advanced Topics

### 🔹 Mocking & Patching
- Use `unittest.mock` to replace parts of your system during testing  
```python
from unittest.mock import patch

@patch("module.requests.get")
def test_api_call(mock_get):
    mock_get.return_value.status_code = 200
    # test code that uses requests.get
```

### 🔹 Property-Based Testing
- Use **hypothesis** to generate inputs automatically  
```python
from hypothesis import given, strategies as st

@given(st.integers(), st.integers())
def test_add_commutative(a, b):
    assert add(a, b) == add(b, a)
```

### 🔹 Performance Testing
- Measure execution time / memory usage
- Libraries: `pytest-benchmark`, `timeit`

### 🔹 Security & Static Analysis
- Tools like `bandit` to catch common security issues  
```bash
pip install bandit
bandit -r project/
```

### 🔹 CI/CD Integration
- Run tests automatically on every commit (GitHub Actions, GitLab CI, Jenkins)  
- Example GitHub Action workflow:
```yaml
name: Python Tests
on: [push]
jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      - uses: actions/setup-python@v4
        with:
          python-version: "3.10"
      - run: pip install -r requirements.txt
      - run: pytest
```

---

## 🔗 References
- [Python unittest docs](https://docs.python.org/3/library/unittest.html)  
- [pytest docs](https://docs.pytest.org/)  
- [coverage.py](https://coverage.readthedocs.io/)  
- [unittest.mock](https://docs.python.org/3/library/unittest.mock.html)  
- [hypothesis](https://hypothesis.readthedocs.io/)  
- [bandit](https://bandit.readthedocs.io/)  
- [Real Python: Python Testing](https://realpython.com/python-testing/)  
