[![Build Status](https://img.shields.io/travis/loopmediagroup/py-gardener/master.svg)](https://travis-ci.org/loopmediagroup/py-gardener)
[![Coverage Status](https://coveralls.io/repos/github/loopmediagroup/py-gardener/badge.svg?branch=master)](https://coveralls.io/github/loopmediagroup/py-gardener?branch=master)
[![Dependencies](https://pyup.io/repos/github/loopmediagroup/py-gardener/shield.svg?t=1518818417448)](https://pyup.io)

# Py-Gardener

Released on [pypi](https://pypi.python.org/pypi/Py-Gardener). Install with

`pip install py-gardener`

### What is Py-Gardener?

Py-Gardener enforces best practices for your python project.

### Run Tests

Check out [SETUP.md](SETUP.md)

### Where can I get help?

Please open a github issue.

-------------------

## Getting Started

- [Test File](#test-file)
- [What are the tests?](#what-are-the-tests?)
  - [Test Incorrect Bool Conditional](#test-incorrect-bool-conditional)
  - [Test Line Endings](#test-line-endings)
  - [Test Pylint](#test-pylint)
  - [Test PEP8](#test-pep8)
  - [Test Structure](#test-structure)
    - [Test Class Names Match](#test-class-names-match)
    - [Test Related Lib File Exists](#test-related-lib-file-exists)
    - [Test Init Files Exist](#test-init-files-exist)
  - [Test Version Consistent](#test-version-consistent)

### Test File


Create the following file:

`$PROJECT_DIR/tests/static/test_gardener.py`

```python
import os
from py_gardener.StaticTestBase import StaticTestBase


class TestGardener(StaticTestBase):
    ROOT_DIR = os.path.join(os.path.dirname(__file__), '..', '..')
    TEST_DIR = os.path.join(ROOT_DIR, "tests")
    LIB_DIR = os.path.join(ROOT_DIR, "service_acl_data")

```

### What are the tests?

#### Test Incorrect Bool Conditional

Test asserts don't check 'in (True, False)' (false positives).

Use `isinstance(val, bool)` instead

#### Test Line Endings

Test that lines do not end with backslash - use parenthesis instead

#### Test PEP8

Test that we conform to PEP8.

#### Test Pylint

Test that we conform to Pylint.

Pylint requires a config to adhere to. 

To generate the default config, run:

     $ pylint --generate-rcfile > .pylintrc

To add different configurations for sub-directories, include a separate `.pylintrc` at the root of the subdirectory.

Example: 

```
$PROJECT_ROOT
|-- Dir1
|    |-- file1.py
|-- Dir2
|    |-- Dir3
|    |    |-- file2.py
|    |-- file3.py
|    |-- .pylintrc
|-- .pylintrc
```

In the above scenario, `file1.py` would be validated against `$PROJECT_ROOT/.pylintrc` whereas `file2.py` & `file3.py` would be validated against `$PROJECT_ROOT/Dir2/.pylintrc`.

Common errors to ignore:
- C0111 (missing-docstring)
- C0103 (invalid-name)
- W0613 (unused-argument)
- R0901 (too-many-ancestors)
- R0903 (too-few-public-methods)
- W0231 (super-init-not-called)

#### Test Structure

##### Test Class Names Match

Test that test class names are correct. (Test class name must match file name)

For example:

`TestExample.py`
```python
import unittest
class TestExample(unittest.TestCase):
    pass
```

##### Test Related Lib File Exists

Check test files have corresponding lib file if folder exists.

##### Test Init Files Exist

Check that each test folder has an init file.

#### Test Version Consistent

*_Only validates if `$PROJECT_ROOT/setup.py` exists_*

Test setup.py version doesn't fall behind git tag.
