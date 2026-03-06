# Password Validator v0.1.1

A modular, rule-based password validation engine written in Python.  
**v0.1.1 Update.** Project now with `uv` to provide an isolated, reproducible environment! 
This ensures consistent behavior across machines without touching system Python.

---
## Features (v0.1.1)

- Validate password length, uppercase, lowercase, digits, special characters 
- Optional space restriction 
- CLI interface using `getpass` (interactive input) 
- Fully tested with `pytest` 
- uv environment for isolated, reproducible Python setup

---
## Project Structure

```text
password-validator/ 
    | 
    ├── src/.
    |    └── password_validator/
    |            ├── __init__.py        # Public API surface
    |            ├── cli.py     # Optional interface
    |            └── validator.py       # Core logic
    ├── tests/
    |    └── test_validator.py      # Test suite
    ├── pyproject.toml   
    ├── README.md
    ├── LICENSE.md
    └──.gitignore
```

---
## Installation and usage with `uv`

This project is designed to be run with `uv` - a fast Python package and project manager that keeps your system Python clean. 

1. Install `uv` (if not already)

Windows PowerShell
``` PowerShell
pip install uv
```
or see [official installation guide](https://docs.astra.sh/uv/getting-started/installation/)

Verify Installation:
``` PowerShell
uv --version
```

2. Clone and enter the repository:

``` bash
git clone https://github.com/botshelo-mere/password-validator.git
cd password-validator
```

3. Setup the project environment

Create and synchronize the isolated Python environment:
``` bash
uv lock # generates uv.lock file 
uv sync # installs Python and dependencies in isolation
```


## Running the CLI

There are two ways to run the CLI.  
From the project root:

#### Option 1 (Development / Debugging)
``` bash
uv run python -m password_validator.cli
```

#### Option 2 (Installed / User-Friendly):
``` bash
uv run validate-password
```

You will be prompted to enter your password:
- If the password is invalid, errors will be displayed
- Repeat until a valid password is created
- Or exit gracefully on Ctrl+C or input interruption

Use Option 1 while developing or debugging, and Option 2 once the environment is synced for general usage


## Running Tests

All tests are located in the `tests/` folder and are written using `pytest`.  
From the project root:

#### Option 1 - Run all tests
``` bash
uv run pytest 
```

#### Option 2 - Run a specific test function
```bash
uv run pytest tests/test_validator.py::test_valid_password
```

**NOTE**: `uv run pytest` works because `pytest` is installed in the uv environment. 
Do not run `python test_validator.py` direclty - the test framework will not discover functions.

The test suite verifies:
- Length boundaries (min and max)
- Character class requirements
- Space restrictions
- Multiple simultaneous rule violations
- Type validation
- Empty input handling
- Configuration toggles

### Library Usage Example

You can use the validator directly in Python code:
``` python
from password_validator import PasswordValidator

validator = PasswordValidator(min_length=12, allow_spaces=True) 
errors = validator.validate("My Password1!") 

if not errors: 
    print("Password is valid!") 
else: 
    print("Password invalid:", errors) 
```

#### Configuration Options

```  python
validator = PasswordValidator(
    min_length=12,
    max_length=32,
    special_chars="!@#$%",
    allow_spaces=True
) 
```

---
## Development Notes

- Use uv run pytest to run all tests
- CLI uses getpass — passwords are not echoed
- Validator logic is pure library, no automatic printing
- Ready for future features (v0.2.0: entropy detection)

---
## Version History

Version 0.1.0
- Initial public release

Version 0.1.1
- Development environment improvements and project documentation

Current Version: Alpha (v0.1.1)

This version improves infrastructure and packaging but does not change core validation logic.

---
## License
This project is licensed under the MIT License - see the [LICENSE](LICENSE.md) file for details.

---
## Author 

Botshelo Mere

Github: [https://github.com/botshelo-mere](https://github.com/botshelo-mere)
