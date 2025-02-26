import random
import string

# Function to load predefined lists of adjectives and nouns
def load_words():
    adjectives = ["Cool", "Happy", "Fast", "Clever", "Brave", "Mighty", "Fierce", "Loyal"]
    nouns = ["Tiger", "Dragon", "Eagle", "Wolf", "Panther", "Falcon", "Cheetah", "Shark"]
    return adjectives, nouns

# Function to generate a random username based on user preferences
def generate_username(include_numbers=True, include_special=False, length=None):
    adjectives, nouns = load_words()
    adj = random.choice(adjectives)
    noun = random.choice(nouns)
    
    username = adj + noun
    
    if include_numbers:
        username += str(random.randint(10, 99))
    
    if include_special:
        special_chars = "!@#$%^&*"
        username += random.choice(special_chars)
    
    if length and len(username) > length:
        username = username[:length]
    
    return username

# Function to save generated usernames to a file
def save_to_file(username, filename="usernames.txt"):
    with open(filename, "a") as file:
        file.write(username + "\n")
    print(f"Username '{username}' saved to {filename}")

# Main function to interact with the user
def main():
    print("Welcome to the Random Username Generator!")
    
    # User preferences input
    include_numbers = input("Include numbers? (yes/no): ").strip().lower() == "yes"
    include_special = input("Include special characters? (yes/no): ").strip().lower() == "yes"
    length = input("Set a maximum username length (press Enter to skip): ").strip()
    length = int(length) if length.isdigit() else None
    
    # Generate username based on user input
    username = generate_username(include_numbers, include_special, length)
    print(f"Generated Username: {username}")
    
    # Option to save the username
    save_option = input("Do you want to save this username? (yes/no): ").strip().lower()
    if save_option == "yes":
        save_to_file(username)
    
# Run the main function if script is executed directly
if __name__ == "__main__":
    main()
