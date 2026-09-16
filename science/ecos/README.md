# Economic Analysis Module - Test Suite

Comprehensive test suite for the Economic Analysis Module based on formal economic theory and system analysis.

## Overview

This project provides a Python implementation of economic analysis concepts from the dissertation work on:
- Resonance window optimization (Ω ∈ [0.618, 0.796])
- Economic uncertainty and stability analysis
- Supply chain optimization
- Market dynamics and filter models
- Harmonic and entropy analysis
- Lyapunov stability metrics

## Project Structure

```
.
├── economic_analysis.py      # Core module
├── pyproject.toml            # Project configuration
├── README.md                 # This file
└── tests/                    # Test suite
    ├── __init__.py
    ├── conftest.py          # Pytest fixtures and configuration
    ├── test_core_functions.py
    ├── test_filter_functions.py
    ├── test_harmonic_analysis.py
    ├── test_advanced_analysis.py
    └── test_integration_and_edge_cases.py
```

## Installation

### Prerequisites

- Python 3.8+
- numpy >= 1.21.0
- scipy >= 1.7.0

### Setup

```bash
# Install in development mode with all dependencies
pip install -e ".[dev,test]"

# Or just install for testing
pip install -e ".[test]"
```

## Running Tests

### Basic Test Execution

```bash
# Run all tests
pytest

# Run with verbose output
pytest -v

# Run specific test file
pytest tests/test_core_functions.py

# Run specific test class
pytest tests/test_core_functions.py::TestResonanceWindow

# Run specific test
pytest tests/test_core_functions.py::TestResonanceWindow::test_window_center
```

### Coverage Analysis

```bash
# Generate coverage report
pytest --cov=economic_analysis --cov-report=html

# View detailed coverage
open htmlcov/index.html  # macOS
xdg-open htmlcov/index.html  # Linux
start htmlcov/index.html  # Windows

# Coverage with detailed output
pytest --cov=economic_analysis --cov-report=term-missing
```

### Parallel Execution

```bash
# Run tests in parallel (faster execution)
pytest -n auto

# Run with specific number of workers
pytest -n 4
```

### Test Markers

```bash
# Run only unit tests
pytest -m unit

# Run only integration tests
pytest -m integration

# Run only edge case tests
pytest -m edge_case

# Skip slow tests
pytest -m "not slow"
```

### Specific Test Scenarios

```bash
# Run tests with output
pytest -v -s

# Run tests with detailed failure info
pytest -vv --tb=long

# Run tests and stop on first failure
pytest -x

# Run tests and show local variables on failure
pytest -l

# Run with specific Python version
python3.9 -m pytest
```

## Test Coverage

The test suite aims for comprehensive coverage:

### Core Functions Tests (`test_core_functions.py`)
- **Classes**: 8 test classes, ~60 test cases
- **Coverage**: 
  - Omega validation and resonance window detection
  - Productivity calculations
  - Freedom degree, predictability, price variance
  - Gini coefficient and growth rate
  - Comprehensive resonance analysis

### Filter Functions Tests (`test_filter_functions.py`)
- **Classes**: 5 test classes, ~40 test cases
- **Coverage**:
  - Cutoff frequency calculations
  - Filter magnitude response
  - Shock response and damping
  - Stability conditions

### Harmonic Analysis Tests (`test_harmonic_analysis.py`)
- **Classes**: 6 test classes, ~50 test cases
- **Coverage**:
  - Leibniz series coefficients and convergence
  - Market supply odd harmonics
  - Fourier rectangle wave reconstruction
  - Market adjustment dynamics

### Advanced Analysis Tests (`test_advanced_analysis.py`)
- **Classes**: 8 test classes, ~70 test cases
- **Coverage**:
  - Historical regime analysis
  - Market entropy and mutual information
  - Lyapunov exponent calculations
  - Supply chain optimization

### Integration & Edge Cases Tests (`test_integration_and_edge_cases.py`)
- **Classes**: 10 test classes, ~80 test cases
- **Coverage**:
  - Cross-function integration
  - Boundary conditions and edge cases
  - Numerical stability
  - Error handling
  - Consistency and monotonicity properties

### Total Coverage
- **~300 test cases** total
- **90%+ code coverage** target
- Tests cover:
  - Normal operation paths
  - Boundary conditions
  - Error cases
  - Edge cases
  - Integration scenarios
  - Numerical stability

## Test Categories

### Unit Tests (`@pytest.mark.unit`)
Individual function tests in isolation:
- Input validation
- Output correctness
- Mathematical properties
- Edge cases

### Integration Tests (`@pytest.mark.integration`)
Tests for interaction between functions:
- Pipeline consistency
- Cross-module behavior
- System-level properties

### Edge Case Tests (`@pytest.mark.edge_case`)
Boundary and special condition tests:
- Extreme values
- Numerical limits
- Special parameter combinations

## Configuration

### pyproject.toml Settings

The `pyproject.toml` file contains comprehensive configuration:

```toml
[tool.pytest.ini_options]
testpaths = ["tests"]
python_files = ["test_*.py"]
addopts = "-v --strict-markers --tb=short"

[tool.coverage.report]
fail_under = 90
exclude_lines = ["pragma: no cover", ...]

[tool.black]
line-length = 100

[tool.mypy]
python_version = "3.8"
```

## Fixtures and Helpers

The `conftest.py` provides reusable fixtures:

```python
# Data fixtures
- valid_omega_values()      # Valid omega test values
- resonance_window_omegas() # Omegas around resonance window
- filter_parameters()       # Filter test parameters
- supply_chain_data()       # Sample supply chain data
- harmonic_parameters()     # Harmonic analysis parameters

# Helper fixtures
- assert_close()           # Floating point comparison
- assert_monotonic()       # Monotonicity assertion
- assert_in_range()        # Range assertion
- benchmark_timer()        # Performance timing
```

## Test Execution Examples

### Full Test Suite with Coverage
```bash
pytest --cov=economic_analysis --cov-report=html -v
```

### Run Critical Tests
```bash
pytest tests/test_core_functions.py tests/test_advanced_analysis.py -v
```

### Continuous Testing
```bash
pytest -n auto --tb=short -q
```

### Development Mode
```bash
pytest -v -s --tb=long tests/test_core_functions.py
```

## Interpreting Results

### Coverage Report

The HTML coverage report shows:
- **Lines covered**: Green
- **Lines not covered**: Red
- **Branches covered**: Yellow

Target: **≥90% coverage**

### Test Output

```
============ test session starts ===========
collected 300 items

tests/test_core_functions.py ...................... [ 10%]
tests/test_filter_functions.py .................... [ 20%]
...
============ 300 passed in 2.34s ============
```

### Failed Tests

If tests fail:
1. Check the error message and traceback
2. Identify the failing assertion
3. Review the test code and function being tested
4. Run with `-v -s` for detailed output
5. Use `--tb=long` for extended traceback

## Performance Testing

```bash
# Time all tests
pytest --durations=10

# Profile specific test
pytest tests/test_core_functions.py::TestResonanceAnalysis -v --profile
```

## Continuous Integration

For CI/CD pipelines:

```bash
# Simple CI command
pytest --cov=economic_analysis --cov-report=xml

# With stricter requirements
pytest --cov=economic_analysis --cov-fail-under=95 -v --tb=short
```

## Troubleshooting

### Import Errors
```bash
# Ensure package is installed
pip install -e ".[dev,test]"

# Check Python path
python -c "import economic_analysis; print(economic_analysis.__file__)"
```

### Coverage Not Showing
```bash
# Reinstall with coverage tools
pip install -e ".[test]" --force-reinstall

# Check coverage installation
python -c "import pytest_cov; print(pytest_cov.__version__)"
```

### Tests Slow/Hanging
```bash
# Add timeout
pytest --timeout=10

# Run specific fast tests
pytest -m "not slow"
```

## Code Quality Tools

Also available through `pyproject.toml`:

```bash
# Format code
black .

# Check imports
isort .

# Lint code
flake8 economic_analysis.py

# Type checking
mypy economic_analysis.py
```

## Contributing

When adding new functions:

1. Write tests first (TDD approach)
2. Ensure 90%+ coverage for new code
3. Run full test suite: `pytest --cov=economic_analysis`
4. Document test coverage goals
5. Add appropriate markers (`@pytest.mark.unit`, etc.)

## References

Test structure based on:
- [pytest documentation](https://docs.pytest.org/)
- [coverage.py documentation](https://coverage.readthedocs.io/)
- Best practices for scientific Python testing

## Author

Developed as comprehensive testing suite for Economic Analysis Module
- Original dissertation: Stephan Epp
- Python implementation and tests: 2026

## License

MIT License - See LICENSE file for details
