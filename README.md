# 02_04 CI for Python


🧪 Automate CI for Python

This project demonstrates a complete Continuous Integration (CI) pipeline for a Python FastAPI application using GitHub Actions.

🚀 Project Overview

This repository automates:

🧱 Linting (with flake8)

🧪 Unit Testing (with pytest)

🧰 Dependency Installation (from requirements.txt)

📦 Workflow execution on every push or pull request

⚙️ CI/CD Workflow Explanation

The main workflow file is located at:

.github/workflows/python-app.yml

🔄 Steps Executed
Step	Description
Checkout Code	Pulls latest code from the repo
Setup Python	Uses Python 3.10 for testing
Install Dependencies	Installs packages from requirements.txt
Lint with flake8	Ensures clean and standardized code
Run Tests	Executes test cases with pytest
Generate Test Report	Displays test summary (pass/fail details)
✅ Test Summary

After fixing version conflicts (httpx==0.27.2), all tests now pass successfully.

Test	Result
test_read_data	✅ Passed
test_read_data_by_guid	✅ Passed
test_read_data_by_invalid_guid	✅ Passed
🧾 Requirements

The compatible requirements.txt:

fastapi==0.92.0
uvicorn==0.20.0
httpx==0.27.2
pytest
flake8

🧰 Commands to Run Locally
1️⃣ Create & Activate Virtual Environment
python -m venv .venv
source .venv/bin/activate   # (Linux/Mac)
.venv\Scripts\activate      # (Windows)

2️⃣ Install Dependencies
pip install -r requirements.txt

3️⃣ Run Tests Locally
pytest -v

⚡ CI Status
Build	Status
Python Application Workflow	✅ Passing
📸 Workflow Screenshots

Click below to view actual workflow screenshots uploaded to your repo’s GitHub folder.

✅ Successful Test Run

✅ All Tests Passed

✅ Final Build Report
## 📸 CI Workflow Screenshots

Below are the screenshots showing your successful GitHub Actions CI build.

| Stage | Screenshot |
|--------|-------------|
| ✅ **Workflow Test Execution** | <img src="./Screenshot%202025-10-18%20151711.png" alt="Workflow Test Execution" width="800"/> |
| ✅ **Build Success Summary** | <img src="./Screenshot%202025-10-18%20151722.png" alt="Build Success Summary" width="800"/> |
| ✅ **JUnit Test Results** | <img src="./Screenshot%202025-10-18%20152226.png" alt="JUnit Test Results" width="800"/> |

> 💡 Make sure the images are located in the same directory as your `README.md`, like:
> ```
> /workspaces/Automate_CI_for_Python/
> ├── README.md
> ├── Screenshot 2025-10-18 151711.png
> ├── Screenshot 2025-10-18 151722.png
> └── Screenshot 2025-10-18 152226.png
> ```

---

### 🧠 Explanation

- `./` means “same folder as README.md”
- `%20` replaces spaces in filenames (Markdown encoding)
- You can adjust `width="800"` to make the screenshots smaller or larger

---

### ✅ Example Preview

| Stage | Screenshot |
|--------|-------------|
| ✅ **Workflow Test Execution** | ![Workflow Test Execution](./Screenshot%202025-10-18%20151711.png) |
| ✅ **Build Success Summary** | ![Build Success Summary](./Screenshot%202025-10-18%20151722.png) |
| ✅ **JUnit Test Results** | ![JUnit Test Results](./Screenshot%202025-10-18%20152226.png) |

---
.

🧠 Notes

The test client warning:

DeprecationWarning: The 'app' shortcut is now deprecated.


is safe and can be ignored for now; newer FastAPI versions will fix it automatically.

CI automatically runs whenever:

You push commits to main

You create a pull request

👏 Credits

Built and maintained by Buvanesh R
Automated and verified via GitHub Actions CI pipeline.



# Permissions for Checks
Permissions are needed to update the Actions interface.  Permissions can be added under the `job` section for a specific job, or at the top of a workflow so all jobs assume the permission.

    jobs:
        build:
            runs-on: ubuntu-latest
            permissions:
                checks: write

# JUnit Reporting
Tests can be updated to include JUnit reports.

Actions can be added to publish JUnit reports to the Actions user interface.

For example, a standard call to `pytest` can be modified from:

    - name: Test with pytest
      run: |
        pytest

to:


    - name: Test with pytest
      run: |
        python -m pytest --verbose --junit-xml=junit.xml
    - name: Publish Test Report
      uses: mikepenz/action-junit-report@v3
      if: success() || failure() # always run even if the previous step fails
      with:
        report_paths: '**/junit.xml'
        detailed_summary: true
        include_passed: true

A complete workflow is located here: [./python-ci-workflow.yml](./python-ci-workflow.yml)
