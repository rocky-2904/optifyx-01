    import re

    class PasswordStrengthChecker:
    def __init__(self, password):
        self.password = password

    def check_length(self):
        return len(self.password) >= 8

    def check_uppercase(self):
        return bool(re.search(r'[A-Z]', self.password))

    def check_lowercase(self):
        return bool(re.search(r'[a-z]', self.password))

    def check_digit(self):
        return bool(re.search(r'[0-9]', self.password))

    def check_special_character(self):
        return bool(re.search(r'[@$!%*?&]', self.password))

    def evaluate_strength(self):
        strength_criteria = {
            'Length >= 8': self.check_length(),
            'Uppercase letter': self.check_uppercase(),
            'Lowercase letter': self.check_lowercase(),
            'Number': self.check_digit(),
            'Special character (@, $, !, %, *, ?, &)': self.check_special_character()
        }

        passed_criteria = sum(strength_criteria.values())
        total_criteria = len(strength_criteria)

        if passed_criteria == total_criteria:
            strength = 'Strong'
        elif passed_criteria >= 3:
            strength = 'Medium'
        else:
            strength = 'Weak'

        print("\nPassword Strength Evaluation:")
        for criteria, passed in strength_criteria.items():
            status = "Passed" if passed else "Failed"
            print(f"{criteria}: {status}")

        print(f"\nOverall Password Strength: {strength}")

    # Example usage:
    password = input("Enter a password to evaluate: ")
    checker = PasswordStrengthChecker(password)
    checker.evaluate_strength()
