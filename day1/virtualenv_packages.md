# 12. Virtual Environments and Packages

## 12.1 Introduction
- Applications may need different versions of the same library → conflict in a single global installation.  
- **Virtual environment** = isolated Python installation with its own dependencies.  
- Different projects can use different package versions without interfering.  

---

## 12.2 Creating Virtual Environments
- Use `venv` module:  
  ```bash
  python -m venv tutorial-env
  ```
  → creates a directory with Python interpreter and libraries.

- **Activation**:  
  - Windows: `tutorial-env\Scripts\activate`  
  - macOS/Linux: `source tutorial-env/bin/activate`

- Example:
  ```bash
  $ source ~/envs/tutorial-env/bin/activate
  (tutorial-env) $ python
  >>> import sys
  >>> sys.path
  [..., '~/envs/tutorial-env/lib/python3.12/site-packages']
  ```

- **Deactivation**:  
  ```bash
  deactivate
  ```

---

## 12.3 Managing Packages with `pip`
- Install latest version:
  ```bash
  python -m pip install novas
  ```
- Install specific version:
  ```bash
  python -m pip install requests==2.6.0
  ```
- Upgrade:
  ```bash
  python -m pip install --upgrade requests
  ```
- Uninstall:
  ```bash
  python -m pip uninstall requests
  ```
- Show package info:
  ```bash
  python -m pip show requests
  ```
- List installed packages:
  ```bash
  python -m pip list
  ```
- Save dependencies:
  ```bash
  python -m pip freeze > requirements.txt
  ```
- Install from file:
  ```bash
  python -m pip install -r requirements.txt
  ```

**Example** `requirements.txt`:
```
novas==3.1.1.3
numpy==1.9.2
requests==2.7.0
```

---

✅ **Key takeaway**:  
- Use **`venv`** to isolate project environments.  
- Use **`pip`** to install/manage dependencies.  
- Use **`requirements.txt`** to share and reproduce environments.  
---
## Reference
- [Python 3 Tutorial — 12. Virtual Environments and Packages](https://docs.python.org/3/tutorial/venv.html) © Python Software Foundation — Licensed under the PSF License v2
