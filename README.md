# Module Lab: Automating Python Projects with Pip, PyPi & Scripting

## Overview

This lab demonstrates how to build a modular Python automation tool using:

- File I/O
- Timestamped output files
- Virtual environments
- Dependency management with pip
- Reproducible environments using requirements.txt
- Git version control workflows

The project focuses on implementing a reusable function called `generate_log()` that creates timestamped log files from a list of entries.



## Project Structure

```
module-lab-pip-pypi-scripting/
│
├── lib/
│ └── generate_log.py
│
├── testing/
│ └── test_generate_log.py
│
├── requirements.txt
└── README.md
```



## Setup Instructions

### Clone the Repository

```
git clone <repo-url>
cd module-lab-pip-pypi-scripting
```


### Create and Activate a Virtual Environment


```
python3 -m venv venv
source venv/bin/activate
```


### Install Dependencies

```
pip install -r requirements.txt
```
Or 
```
pip install pytest requests
pip freeze > requirements.txt
```


## Core Implementation

### The `generate_log()` Function

- Validates that input is a list
- Raises a `ValueError` for invalid input
- Generates a timestamped filename in the format:


log_YYYYMMDD.txt


- Writes each log entry on a new line
- Prints a confirmation message
- Returns the filename for testing


### Implementation (`lib/generate_log.py`)


from datetime import datetime
import os

def generate_log(data):
if not isinstance(data, list):
raise ValueError("Input must be a list.")

today = datetime.now().strftime("%Y%m%d")
filename = f"log_{today}.txt"

with open(filename, "w") as file:
    for entry in data:
        file.write(f"{entry}\n")

print(f"Log written to {filename}")
return filename

if name == "main":
sample_data = ["User logged in", "User updated profile", "Report exported"]
generate_log(sample_data)



## Running the Script

From the project root directory:

```
python lib/generate_log.py
```

Expected output:

```
Log written to log_YYYYMMDD.txt
```


## Running Tests

This project uses pytest.

```
pytest
```

Expected result:

```
5 passed
```

The test suite verifies:

- The log file is created
- The filename format is correct
- File contents exactly match the input list
- A `ValueError` is raised for invalid input
- An empty list creates a valid empty file


## Dependency Management

To ensure reproducibility:

```
pip freeze > requirements.txt
```

This allows the environment to be recreated exactly on any system.



## Git Workflow

Create a feature branch:

```
git checkout -b feature-automation-tool
```

Commit changes:

```
git add .
git commit -m "Implement generate_log function"
```

Merge using the terminal:

```
git checkout main
git merge feature-automation-tool
git push origin main
```


## Best Practices Applied

- Input validation using `isinstance`
- Error handling with `ValueError`
- Modular script design
- Clean entry point using:


if name == "main":


- Dependency tracking with requirements.txt
- Virtual environment isolation
- Git branch-based workflow
