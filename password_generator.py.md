import random
import string

def generate_password(length=12, use_uppercase=True, use_digits=True, use_special=True):
    """Generate a random password with specified complexity."""
    characters = string.ascii_lowercase
    if use_uppercase:
        characters += string.ascii_uppercase
    if use_digits:
        characters += string.digits
    if use_special:
        characters += string.punctuation
    
    # Ensure password meets complexity requirements
    while True:
        password = ''.join(random.choice(characters) for _ in range(length))
        if (not use_uppercase or any(c.isupper() for c in password) and \
           (not use_digits or any(c.isdigit() for c in password) and \
           (not use_special or any(c in string.punctuation for c in password))):
            break
    
    return password

def get_user_input():
    """Get password requirements from user."""
    print("=== Password Generator ===")
    try:
        length = int(input("Enter password length (8-64): "))
        if length < 8 or length > 64:
            print("Length must be between 8 and 64. Using default 12.")
            length = 12
        
        uppercase = input("Include uppercase letters? (y/n): ").lower() == 'y'
        digits = input("Include digits? (y/n): ").lower() == 'y'
        special = input("Include special characters? (y/n): ").lower() == 'y'
        
        return length, uppercase, digits, special
    except ValueError:
        print("Invalid input. Using default settings.")
        return 12, True, True, True

def main():
    length, uppercase, digits, special = get_user_input()
    password = generate_password(length, uppercase, digits, special)
    print("\nGenerated Password:")
    print(password)

if __name__ == "__main__":
    main()
