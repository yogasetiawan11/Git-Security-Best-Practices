# Pre-commit framework
The pre-commit framework uses Gitleaks to identify any sensitive information in your repo. 
Here are steps to implement it: 
## Replace the pre-commit hook with Gitleaks 
### 1. Download Pre-commit framework using pip 
https://pre-commit.com/#install
```sh 
pip install pre-commit 
```
### 2. Create pre-commit configuration at the root of repository
```yaml
repos:
  - repo: https://github.com/gitleaks/gitleaks
    rev: v8.24.2
    hooks:
      - id: gitleaks 
```
### 3. Auto-update the config to the latest repos' versions by executing `pre-commit autoupdate`
### 4. Install with `pre-commit install`
### 5. Now you're all set!

This showcase that pre-commit calling gitleaks, and It will handle the script wrote in the previous case. And the other advantage is that it can work on all repositories and different pattern that you have.