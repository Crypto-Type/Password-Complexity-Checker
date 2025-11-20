# Password-Complexity-Checker
Password Security Criteria

import re

def password_strength(password):
    strength = 0
    feedback = []

    # Criteria
    length_criteria = len(password) >= 8
    upper_criteria = re.search(r"[A-Z]", password) is not None
    lower_criteria = re.search(r"[a-z]", password) is not None
    digit_criteria = re.search(r"[0-9]", password) is not None
    special_criteria = re.search(r"[!@#$%^&*()_+\-=\[\]{}|;:',.<>/?]", password) is not None

    # Feedback and scoring
    if length_criteria:
        strength += 1
    else:
        feedback.append("Password should be at least 8 characters long.")
    if upper_criteria:
        strength += 1
    else:
        feedback.append("Add at least one uppercase letter.")
    if lower_criteria:
        strength += 1
    else:
        feedback.append("Add at least one lowercase letter.")
    if digit_criteria:
        strength += 1
    else:
        feedback.append("Include at least one numeric digit.")
    if special_criteria:
        strength += 1
    else:
        feedback.append("Use at least one special character (e.g. !, @, #, $, etc.).")

    # Strength rating
    if strength == 5:
        verdict = "Strong password."
    elif strength >= 3:
        verdict = "Moderate password."
    else:
        verdict = "Weak password."

    return verdict, feedback

# User input
password = input("Enter your password: ")
verdict, suggestions = password_strength(password)
print(f"\nPassword Strength: {verdict}")
if suggestions:
    print("Suggestions:")
    for tip in suggestions:
        print(f"- {tip}")
else:
    print("Your password meets all recommended criteria!")
