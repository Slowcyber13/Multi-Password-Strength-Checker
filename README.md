# Multi-Password-Strength-Checker
A Python tool to help evaluating and improving password strength
# Password Strength Checker Tool

## Project Goals
- Build a Python tool to automate password strength evaluation for security-conscious users.
- Assess password strength based on critical factors: length, character variety, and use of numbers/special characters.
- Provide actionable feedback and generate secure suggestions for weak passwords automatically.

## Problem Statement
Weak passwords remain a major security vulnerability, compromising personal and organizational data. Users often create insecure passwords due to poor awareness. This tool will automate password strength evaluation and suggest improvements, helping users adopt stronger passwords.

## Expected Outcomes and Deliverables
- Deliverable 1: A Python-based password strength checker that evaluates multiple passwords in a single run.
- Deliverable 2: Well-documented code with a README guide, hosted on a GitHub repository.
- Deliverable 3: A demonstration video showing the tool’s usage and functionality, included with the final submission.

## Timeline
| Task                              | Deliverable                                | Timeline   |
|-----------------------------------|--------------------------------------------|------------|
| Project Plan & Scope              | Complete project outline                   | Day 1–2    |
| Design & Development              | Write and enhance the password checker code| Day 3–5    |
| Testing & Debugging               | Test the tool on multiple platforms        | Day 6–7    |
| Documentation & GitHub Setup      | Upload code, create README, and set up repository | Day 8–9 |
| Final Demo & Submission           | Record demo video and prepare report      | Day 10–12  |

## Why This Solution Works

	•	Multiple Password Handling: Users can assess multiple passwords in a single run.
	•	Automated Password Generation: Weak passwords (score ≤ 2) trigger a secure password suggestion.
	•	Clear Feedback: Every password gets detailed feedback to guide improvement.
	•	Compatibility: This tool runs smoothly in various Python environments, including PyCharm and mobile editors.


## Code: Password Strength Checker for Multiple Passwords

```python
import re
import random
import string

def check_password_strength(password):
    """Evaluates the strength of a password and provides detailed feedback."""
    score = 0
    missing_criteria = []

    # Length check
    if len(password) >= 12:
        score += 2
    elif len(password) >= 8:
        score += 1
        missing_criteria.append("Increase the length to at least 12 characters.")
    else:
        missing_criteria.append("Use at least 8 characters.")

    # Uppercase and lowercase letters check
    if re.search(r'[A-Z]', password) and re.search(r'[a-z]', password):
        score += 2
    else:
        missing_criteria.append("Include both uppercase and lowercase letters.")

    # Numbers check
    if re.search(r'\d', password):
        score += 1
    else:
        missing_criteria.append("Add at least one number.")

    # Special characters check
    if re.search(r'[!@#$%^&*(),.?":{}|<>]', password):
        score += 2
    else:
        missing_criteria.append("Add at least one special character (e.g., @, #, !).")

    # Display results for each password
    print(f"\nPassword: {password}")
    print(f"Password Score: {score}/7")

    if score == 7:
        print("✅ This password is strong!")
    else:
        print("❌ This password needs improvement. Here's what to add:")
        for criterion in missing_criteria:
            print(f"- {criterion}")

        # Automatically generate a strong password if the score is 2 or lower
        if score <= 2:
            print("\n⚠️ This password is too weak. A strong password has been generated:")
            print(f"🔑 {generate_password()}")

def generate_password(length=12):
    """Generates a secure password with mixed characters."""
    characters = string.ascii_letters + string.digits + string.punctuation
    password = ''.join(random.choice(characters) for _ in range(length))
    return password

def check_multiple_passwords():
    """Allows the user to check the strength of multiple passwords."""
    passwords = input("Enter passwords separated by commas: ").split(',')
    for password in passwords:
        check_password_strength(password.strip())

if __name__ == "__main__":
    print("Welcome to the Password Strength Checker!")
    check_multiple_passwords()

