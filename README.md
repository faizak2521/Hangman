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

std::string wordList();
void guess();

int main() {

    cout << "Welcome to HANGMAN!" << endl << endl;
    cout <<"|---------| " << endl <<
           "|         |" << endl <<
           "| " << endl <<
           "| "<< endl <<
           "| "<< endl <<
           "| "<< endl <<
           "^^^^^^^^^^^^"<< endl;

    //call random words list
    wordList();
    guess();
    return 0;
}


                                //++++++Game Setup+++++++
            // Fix loop to end after winning **DONE**
            //*****Make the animations come in play++++++++


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
//initialize placeholder within new variable
std::string wordGuessed(chosenWord.length(), '_');

    // incorrect guesses
    int incorrectGuesses = 0;
    int guessesAllowed = 6; // const because this won't change

    // Game loop word checking logic
    while(incorrectGuesses != guessesAllowed){


        //Display for initialized placeholder and guesses
        cout << "Word: " << wordGuessed << endl; // Initialized placeholder
        cout << "Guesses Left: " << guessesAllowed << endl; // Guesses

        //Prompt for user to guess
        cout << "Guesses(input letter): ";
        char guess;     // to save user letter guess
        cin >> guess;   //Storing it
        cout << "\n";


        // Validate and check guess
        bool correctGuess = false;
        for (int i = 0; i <= chosenWord.length(); ++i){
            if (chosenWord[i] == guess) {
                wordGuessed[i] = guess;
                correctGuess = true; // Mark as correct
            }
        }

        if (!correctGuess){
            --guessesAllowed;
        }

        if (wordGuessed == chosenWord) {
            cout << "You have won!" << endl;
            return;
        }
    }

    // If exits loop they lost
    cout << "You lost the answer was " << chosenWord << endl;
}


