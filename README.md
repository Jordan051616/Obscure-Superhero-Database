# Obscure-Superhero-Database
//Author: Jordan Garcia
//Assignemnt: Obscure Superhero Database
//Description: Students will build a C++ superhero database that stores and manipulates information about lesser-known superheroes. The program will allow users to search, sort, and analyze superhero data using multidimensional and parallel arrays, along with string manipulation functions.


# #include <iostream>
#include <string>
#include <algorithm> // for sort
#include <cctype>    // for toupper, tolower
using namespace std;

const int NUM_HEROES = 10;


string names[NUM_HEROES] = {
    "Squirrel Girl", "Arm-Fall-Off-Boy", "The Tick", "Matter-Eater Lad",
    "Madame Fatal", "Dogwelder", "Razorback", "Danny the Street",
    "Zeitgeist", "Doorman"
};

string superpowers[NUM_HEROES] = {
    "Control Squirrels", "Detachable Limbs", "Super Strength", "Eat Anything",
    "Disguise", "Weld Dogs", "Drive Anything", "Teleportation",
    "Acid Vomit", "Create Doorways"
};

string weaknesses[NUM_HEROES] = {
    "Time Limits", "Heavy Objects", "Poor Judgment", "Overeating",
    "Old Age", "Fire", "Loud Noises", "Potholes",
    "Digestive Pain", "Walls"
};

string details[NUM_HEROES][2] = {
    {"1992", "Marvel"}, {"1989", "DC"}, {"1986", "Other"},
    {"1962", "DC"}, {"1940", "DC"}, {"1996", "DC"},
    {"1977", "Marvel"}, {"1990", "DC"}, {"2001", "Marvel"},
    {"1989", "Marvel"}
};

string toLower(string s) {
    for (char &c : s) c = tolower(c);
    return s;
}

string toUpper(string s) {
    for (char &c : s) c = toupper(c);
    return s;
}

void displayHeroes(bool uppercase) {
    for (int i = 0; i < NUM_HEROES; i++) {
        string name = names[i];
        string power = superpowers[i];
        string weakness = weaknesses[i];
        string year = details[i][0];
        string universe = details[i][1];

        if (uppercase) {
            name = toUpper(name);
            power = toUpper(power);
            weakness = toUpper(weakness);
            year = toUpper(year);
            universe = toUpper(universe);
        } else {
            name = toLower(name);
            power = toLower(power);
            weakness = toLower(weakness);
            year = toLower(year);
            universe = toLower(universe);
        }

        cout << name << " | " << power << " | " << weakness
             << " | " << year << " | " << universe << endl;
    }
}

void searchByName(string query) {
    query = toLower(query);
    bool found = false;
    for (int i = 0; i < NUM_HEROES; i++) {
        if (toLower(names[i]).find(query) != string::npos) {
            cout << names[i] << " | " << superpowers[i] << " | " << weaknesses[i]
                 << " | " << details[i][0] << " | " << details[i][1] << endl;
            found = true;
        }
    }
    if (!found) cout << "No superhero found with that name.\n";
}

void searchByPower(string powerQuery) {
    powerQuery = toLower(powerQuery);
    bool found = false;
    for (int i = 0; i < NUM_HEROES; i++) {
        if (toLower(superpowers[i]).find(powerQuery) != string::npos) {
            cout << names[i] << " | " << superpowers[i] << " | " << weaknesses[i]
                 << " | " << details[i][0] << " | " << details[i][1] << endl;
            found = true;
        }
    }
    if (!found) cout << "No superheroes found with that superpower.\n";
}

void sortHeroes() {
    for (int i = 0; i < NUM_HEROES - 1; i++) {
        for (int j = i + 1; j < NUM_HEROES; j++) {
            if (toLower(names[i]) > toLower(names[j])) {
                swap(names[i], names[j]);
                swap(superpowers[i], superpowers[j]);
                swap(weaknesses[i], weaknesses[j]);
                swap(details[i][0], details[j][0]);
                swap(details[i][1], details[j][1]);
            }
        }
    }
    cout << "Heroes sorted alphabetically.\n";
}

void showMenu() {
    cout << "\nSuperhero Database Menu:\n";
    cout << "1. Search by name\n";
    cout << "2. Search by superpower\n";
    cout << "3. Sort alphabetically\n";
    cout << "4. Display all (uppercase)\n";
    cout << "5. Display all (lowercase)\n";
    cout << "6. Exit\n";
    cout << "Choose an option (1-6): ";
}

int main() {
    int choice;
    string input;

    do {
        showMenu();
        cin >> choice;
        cin.ignore(); // flush newline
        switch (choice) {
            case 1:
                cout << "Enter superhero name to search: ";
                getline(cin, input);
                searchByName(input);
                break;
            case 2:
                cout << "Enter superpower to search for: ";
                getline(cin, input);
                searchByPower(input);
                break;
            case 3:
                sortHeroes();
                break;
            case 4:
                displayHeroes(true);
                break;
            case 5:
                displayHeroes(false);
                break;
            case 6:
                cout << "Goodbye!\n";
                break;
            default:
                cout << "Invalid option. Try again.\n";
        }
    } while (choice != 6);

    return 0;
}
