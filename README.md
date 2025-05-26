<h1 align="center">flask-route-checker</h1>
<p align="center">
  <em>CLI to detect ⚠️ and auto-fix 🔧 broken <code>url_for()</code> calls in your Flask templates.</em><br>
  <a href="https://pypi.org/project/flask-route-checker/"><img src="https://badge.fury.io/py/flask-route-checker.svg" /></a>
</p>

## 🔍 What It Does

**`flask-route-checker`** is a CLI tool that scans your Jinja templates for broken `url_for()` calls and optionally auto-fixes them by suggesting or replacing with valid endpoint names.

---


## Fixed routes
<h3>Before</h3>
<img src="https://raw.githubusercontent.com/sidiq20/flask-routes-checker/master/docs/fix.png" width="600" />

<h3>After</h3>
<img src="https://raw.githubusercontent.com/sidiq20/flask-routes-checker/master/docs/fixed.png" width="600" />



## ✨ Features


- ✅ Scans all `.html` templates for `url_for()` usage  
- 🚨 Flags endpoints that don’t exist  
- 🔧 `--fix` mode rewrites broken templates and creates backups  
- 🎨 Colorized CLI output, dry-run diff viewer, and ignore filters  
- 📄 Export results as JSON or Markdown reports  
- 🧹 Detects unused routes  
- 🌍 Optional `<a href>` external link checker  
- 🏗️ Works with both:
  - `app = Flask(__name__)`
  - App factory pattern: `create_app()` or custom factory

---
## Quick start



```bash
# install
pip install flask-route-checker
```

# run from your Flask project root
```
flask-route-checker                       # just report issues
```
```
flask-route-checker --fix --backup-dir .backups
```

# Common Setup Scenarios
if you use a factory pattern or non-standard structure, set the edntry point and templates explicity
```
flask-route-checker \
  --app run.py \
  --factory create_app \
  --templates app/templates
```

# possible erros 
ModuleNotFoundError: No module named 'routes'
two ways to fix 

1. run flask-route-checker from project root + add . to PYTHONPATH
    just run this from the same directory as app.py:
    ```
    set PYTHONPATH=.
    flask-route-checker --app app.py # or you main file that runs your flask app 
    ```

    if you are on GIT BASH ot UNIX:
    ```
    PYTHONPATH=. flask-route-checker --app app.py

2. Turn your routes/ into a proper python package
Make sure the routes/ folder has an __init__.py:

## for a diffrent or a robust project structure 

# From your Flask project root, just scan for broken routes:
```
flask-route-checker
```

# Fix all broken routes (backups saved before changes)
```
flask-route-checker --fix --backup-dir .backups
```

touch routes/__init__.py to make it easier 

| Flag                     | Description                                       |                                |
| ------------------------ | ------------------------------------------------- | ------------------------------ |
| `--app PATH`             | Path to entry point file (default: `app.py`)      |                                |
| `--factory NAME`         | If using app factory, name of factory function    |                                |
| `--templates PATH`       | Templates directory (default: `templates`)        |                                |
| `--fix`                  | Automatically fix broken routes                   |                                |
| `--dry-run`              | Show what would change but don’t apply            |                                |
| `--backup-dir DIR`       | Backup fixed templates to this directory          |                                |
| `--ignore-endpoint TEXT` | Skip endpoints containing this text (repeatable)  |                                |
| `--ignore-template TEXT` | Skip templates matching this path fragment        |                                |
| \`--report json          | markdown\`                                        | Output machine-readable report |
| `--unused`               | Show defined routes that aren’t used in templates |                                |
| `--diff`                 | Show unified diff for changes (needs `rich`)      |                                |
| `--fail-on-broken`       | Exit with code 1 if broken routes remain          |                                |
| `--check-external`       | Check <a href> links in templates (slow)          |                                |
| `--verbose`              | Show extra output for debugging                   |                                |
| `--quiet`                | Silence all non-critical output                   |                                |




<h1 align="center">🤝 Contributing</h1>
1. Fork 🚀</br>
2. git clone your fork </br>
3. pip install -e .[dev]</br>
4. Create a branch feat/my-awesome-thing</br>
5. PRs welcome! (Add test if you can)</br>




# Common Isses and fixes
```
ModuleNotFoundError: No module named 'routes'
```
## two ways to fix 

# 🧞‍♂️ ADIOS AMIGO