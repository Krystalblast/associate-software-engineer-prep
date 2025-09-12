# Using the Python Interpreter

## 🔹 Invoking the Interpreter
- Installed usually as `/usr/local/bin/python3.13` on Unix.
- Start with:
  ```bash
  python3.13
  ```
- On Windows:
  - `python3.13` if installed from Microsoft Store.
  - `py` if the Python launcher is installed.

- Exit with:
  - `Ctrl+D` (Unix) or `Ctrl+Z` (Windows)
  - Or `quit()`

- Command line editing depends on system (GNU Readline support).

---

## 🔹 Running Python
- Interactive mode when no file is given.
- Run a command:
  ```bash
  python -c "print('hello')"
  ```
- Run a module:
  ```bash
  python -m module_name
  ```
- Run a script and stay interactive:
  ```bash
  python -i script.py
  ```

---

## 🔹 Argument Passing (`sys.argv`)
- `sys.argv` is a list of strings with script name + arguments.
- Examples:
  - `python script.py test` → `['script.py', 'test']`
  - With `-c` → `sys.argv[0] = '-c'`
  - With `-m module` → `sys.argv[0] = 'module'`

---

## 🔹 Interactive Mode
- Prompts:
  - Primary → `>>>`
  - Continuation → `...`
- Shows version + copyright.
- Example:
  ```python
  the_world_is_flat = True
  if the_world_is_flat:
      print("Be careful not to fall off!")
  ```

---

## 🔹 Source Code Encoding
- Default: UTF-8.
- Use another encoding with:
  ```python
  # -*- coding: encoding -*-
  ```
- Example for Windows-1252:
  ```python
  # -*- coding: cp1252 -*-
  ```
- If using a shebang (`#!/usr/bin/env python3`), put encoding on the second line.

---

## 📖 Reference
- [Python 3 Tutorial — Using the Python Interpreter](https://docs.python.org/3/tutorial/interpreter.html)
