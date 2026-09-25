# CCCS 106: Scholarship Intake Portal

This project implements a Flet-based scholarship application form for the CSPC Scholarship Intake Portal. It applies multi-tier validation, domain-level exception handling, and reactive UI feedback to ensure only valid data is accepted before submission.

## Laboratory Overview

The portal captures the following required fields:

- Full name
- Student ID
- Institutional email
- Mobile number
- GWA
- Scholarship program

The system validates each field using regular expressions, custom exceptions, and defensive parsing. Invalid input triggers inline error messages in the form, and valid submissions create an immutable `ScholarshipApplicant` dataclass instance.

## Project Goals

- Validate input according to CSPC scholarship requirements
- Enforce institutional email and student ID rules
- Safely parse and check GWA values
- Prevent crashes from invalid or non-numeric input
- Provide real-time error clearing in the UI
- Instantiate a validated domain model before persistence

## Validation Rules

### Name
- Required
- 2 to 60 characters
- Allows letters, spaces, periods, hyphens, and apostrophes

### Student ID
- Must match: `^20\d{2}-\d{4,5}$`
- Example: `2024-0123`

### Email
- Must be institutional: `@cspc.edu.ph`
- Example: `maria.santos@cspc.edu.ph`

### Mobile Number
- Must match: `^(?:\+63|0)9\d{9}$`
- Accepts `09181234567` or `+639181234567`

### GWA
- Must be a numeric value between `1.00` and `5.00`
- Invalid values such as `uno` or `0.75` are rejected

### Program
- Must be selected from an accredited scholarship program

## Project Structure

```text
cccs106-lab-form-validation-AASA/
├── README.md
├── scholarship_portal.py
├── test_validation.py
├── .venv/
└── __pycache__/
```

## Requirements

- Python 3.12+
- Flet SDK
- Standard library modules: `re`, `dataclasses`, `datetime`, `typing`, `unittest`

## How to Run

### 1. Open a terminal in the project folder

```bash
cd c:\Users\Victoria Casey\Documents\App Dev Alano\cccs106-lab-form-validation-AASA\cccs106-lab-form-validation-AASA
```

### 2. Create and activate a virtual environment

Windows (PowerShell):

```powershell
python -m venv .venv
.\.venv\Scripts\Activate.ps1
```

Windows (Command Prompt):

```cmd
python -m venv .venv
.venv\Scripts\activate.bat
```

macOS/Linux:

```bash
python3 -m venv .venv
source .venv/bin/activate
```

### 3. Install dependencies

```bash
pip install flet
```

### 4. Run the application

```bash
python scholarship_portal.py
```

This launches the CSPC Scholarship Intake Portal UI.

## Run the Automated Tests

```bash
python test_validation.py -v
```

The project includes a headless validation test suite covering:

- valid and invalid names
- valid and invalid student IDs
- institutional email validation
- mobile number normalization and rejection
- GWA numeric parsing and boundary checks
- dataclass immutability
- GUI submission flow simulation

## Notes on the Implementation

The application uses a multi-tier validation model:

1. UI layer - Flet form and live error feedback
2. Validation engine - regex and defensive parsing logic
3. Domain model - immutable `ScholarshipApplicant` dataclass with custom exceptions

This separation helps prevent crashes and keeps validation rules centralized and maintainable.

## Example Output

When the form submits successfully, the app shows a green floating snackbar with a message such as:

```text
Application accepted for Maria Clara Santos!
```

When validation fails, the relevant fields show red error states and the app does not crash on malformed input.

## Authoring Notes

This project was developed as part of the CCCS 106 Week 5 laboratory exercise on form validation and defensive programming in Flet.
