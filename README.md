```cpp/*Hangman Project
* 6 tries till full hangman is hanged
* A-Z 26 choices
* Random word generator
  */

/*Hangman Project
* 6 tries till full hangman is hanged
* A-Z 26 choices
* Random word generator
  */

// Libraries
#include <iostream>
#include <random>
#include <string>
#include <vector>
#include <iomanip> // for std::setw
using namespace std;

// Definitions
std::string wordList();
void guess();
void hangmanDisplay(int);


int main() {
cout << "Welcome to HANGMAN!" << endl << endl;

    //call random words list
    hangmanDisplay(0);
    wordList();
    guess();
    return 0;
}


//Function for making hangman
void hangmanDisplay(int incorrectGuesses) {

    switch (incorrectGuesses) {
        case 0:
            cout <<"|---------| " << endl <<
                   "|         |" << endl <<
                   "| " << endl <<
                   "| " << endl <<
                   "| "<< endl <<
                   "| "<< endl <<
                   "| "<< endl <<
                   "^^^^^^^^^^^^"<< endl;
            break; // Add break to avoid fall-through
        case 1:
            cout <<"|---------| " << endl <<
                   "|         |" << endl <<
                   "|         0" << endl <<
                   "| " << endl <<
                   "| "<< endl <<
                   "| "<< endl <<
                   "| "<< endl <<
                   "^^^^^^^^^^^^"<< endl;
            break;

        case 2:
            cout <<"|---------| " << endl <<
                   "|         |" << endl <<
                   "|         0" << endl <<
                   "|         |" << endl <<
                   "| "<< endl <<
                   "| "<< endl <<
                   "| "<< endl <<
                   "^^^^^^^^^^^^"<< endl;
            break;

        case 3:
            cout <<"|---------| " << endl <<
                   "|         |" << endl <<
                   "|         0" << endl <<
                   "|         |" << endl <<
                   "|        /" << endl <<
                   "| "<< endl <<
                   "| "<< endl <<
                   "^^^^^^^^^^^^"<< endl;
            break;

        case 4:
            cout <<"|---------| " << endl <<
                   "|         |" << endl <<
                   "|         0" << endl <<
                   "|         |" << endl <<
                   "|        / \\" << endl <<
                   "| "<< endl <<
                   "| "<< endl <<
                   "^^^^^^^^^^^^"<< endl;
            break;

        case 5:
            cout <<"|---------| " << endl <<
                   "|         |" << endl <<
                   "|         0" << endl <<
                   "|         |\\" << endl <<
                   "|        / \\" << endl <<
                   "| "<< endl <<
                   "| "<< endl <<
                   "^^^^^^^^^^^^"<< endl;
            break;

        case 6:
            cout <<"|---------| " << endl <<
                   "|         |" << endl <<
                   "|         0" << endl <<
                   "|        /|\\" << endl <<
                   "|        / \\" << endl <<
                   "| "<< endl <<
                   "| "<< endl <<
                   "^^^^^^^^^^^^"<< endl;
            break;
    }
}


// Function for the random words
std::string wordList() {
// Vector to store list for game
vector<string> listGame = {"gunshot", "titan", "mountain", "rain", "sunset"};

    // Initialize a random number generator with the current time as the seed
    std::default_random_engine generator(std::time(0));
    std::uniform_int_distribution<int> distribution(0, listGame.size() - 1);

    // Randomly pick a word from the list using the distribution
    int randomIndex = distribution(generator);
    std::string chosenWord = listGame[randomIndex];

    // Return the chosen word
    return chosenWord;
}


// Function for the guessing right and wrong
void guess() {
string chosenWord = wordList();
// Initialize placeholder for guessed word
std::string wordGuessed(chosenWord.length(), '_');

    // Initialize incorrect guesses and allowed guesses
    int incorrectGuesses = 0;
    const int maxGuesses = 6; // Constant because it won't change

    // Game loop for word checking logic
    while(incorrectGuesses < maxGuesses) {

        // Display current guessed word and remaining attempts
        cout << "Word: " << wordGuessed << endl;
        cout << "Guesses Left: " << maxGuesses - incorrectGuesses << endl;

        // Prompt the user to guess
        cout << "Guess a letter: ";
        char guess;
        cin >> guess;
        cout << "\n";

        // Validate the user's guess
        bool correctGuess = false;
        for (int i = 0; i < chosenWord.length(); ++i) {
            if (chosenWord[i] == guess) {
                wordGuessed[i] = guess;
                correctGuess = true;
            }
        }

        // If the guess is wrong, update the hangman display and guesses left
        if (!correctGuess) {
            incorrectGuesses++;
            hangmanDisplay(incorrectGuesses);
        }

        // If the word is fully guessed, the player wins
        if (wordGuessed == chosenWord) {
            cout << "You won! The word was " << chosenWord << "." << endl;
            return;
        }
    }

    // If the loop exits, the player lost
    cout << "You lost! The word was " << chosenWord << "." << endl;
}

//Done
```
