# Hangman-Gameimport random

def choose_word():
    """Selects a random word from a predefined list."""
    words = ["apple", "banana", "cherry", "date", "elderberry", "fig", "grape"]
    return random.choice(words)

def display_word(secret_word, guessed_letters):
    """Displays the current state of the word with correctly guessed letters."""
    display = ""
    for letter in secret_word:
        if letter in guessed_letters:
            display += letter + " "
        else:
            display += "_ "
    return display.strip()

def hangman():
    """Main function to run the Hangman game."""
    secret_word = choose_word()
    word_length = len(secret_word)
    guessed_letters = set()
    incorrect_guesses = 0
    max_attempts = 6  # You can adjust the number of allowed incorrect guesses

    print("Welcome to Hangman!")
    print(f"The secret word has {word_length} letters.")
    print(display_word(secret_word, guessed_letters))
    print(f"You have {max_attempts} attempts remaining.")
    print("-" * 20)

    while incorrect_guesses < max_attempts:
        guess = input("Guess a letter: ").lower()

        if not guess.isalpha() or len(guess) != 1:
            print("Invalid input. Please enter a single letter.")
            continue
        elif guess in guessed_letters:
            print("You've already guessed that letter. Try again.")
            continue

        guessed_letters.add(guess)

        if guess in secret_word:
            print("Correct guess!")
            current_display = display_word(secret_word, guessed_letters)
            print(current_display)
            if "_" not in current_display:
                print("Congratulations! You guessed the word:", secret_word)
                break
        else:
            incorrect_guesses += 1
            print(f"Incorrect guess. You have {max_attempts - incorrect_guesses} attempts remaining.")
            print(display_word(secret_word, guessed_letters))

        print("-" * 20)

    if incorrect_guesses == max_attempts:
        print("You ran out of attempts!")
        print("The secret word was:", secret_word)

if __name__ == "__main__":
    hangman()
