# ci-pipeline-playbook

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)
![Python](https://img.shields.io/badge/python-3.11-blue)
![Pytest](https://img.shields.io/badge/pytest-tested-brightgreen)
![CI](https://img.shields.io/badge/CI-GitHub%20Actions-blue)

--> CI pipeline demo with pytest + HTML report.

### Features
- Runs pytest with HTML report
- GitHub Actions workflow uploads `report.html` as artifact

### Run locally
```bash
pip install -r requirements.txt
pytest -q --html=report.html --self-contained-html


**.github/workflows/ci.yml**
```yaml
name: CI Pipeline

on: [push, pull_request]

jobs:
  test:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      - name: Set up Python
        uses: actions/setup-python@v4
        with:
          python-version: '3.11'
      - name: Install dependencies
        run: pip install -r requirements.txt
      - name: Run tests with pytest
        run: pytest -q --html=report.html --self-contained-html
      - name: Upload HTML report
        uses: actions/upload-artifact@v3
        with:
          name: pytest-report
          path: report.html
