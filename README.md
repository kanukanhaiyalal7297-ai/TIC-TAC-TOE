#include <iostream>
using namespace std;

char board[3][3] = {{'1','2','3'},{'4','5','6'},{'7','8','9'}};
char currentMark = 'X';
int currentPlayer = 1;

void displayBoard() {
    cout << "\n";
    for (int i = 0; i < 3; i++) {
        for (int j = 0; j < 3; j++) {
            cout << " " << board[i][j];
            if (j < 2) cout << " |";
        }
        cout << "\n";
        if (i < 2) cout << "---|---|---\n";
    }
    cout << "\n";
}

bool checkWin() {
    for (int i = 0; i < 3; i++)
        if (board[i][0] == board[i][1] && board[i][1] == board[i][2]) return true;
    for (int i = 0; i < 3; i++)
        if (board[0][i] == board[1][i] && board[1][i] == board[2][i]) return true;
    if (board[0][0] == board[1][1] && board[1][1] == board[2][2]) return true;
    if (board[0][2] == board[1][1] && board[1][1] == board[2][0]) return true;
    return false;
}

bool checkDraw() {
    for (int i = 0; i < 3; i++)
        for (int j = 0; j < 3; j++)
            if (board[i][j] != 'X' && board[i][j] != 'O') return false;
    return true;
}

bool markBoard(int choice) {
    if (choice < 1 || choice > 9) return false;
    int row = (choice - 1) / 3;
    int col = (choice - 1) % 3;
    if (board[row][col] == 'X' || board[row][col] == 'O') return false;
    board[row][col] = currentMark;
    return true;
}

int main() {
    int choice;
    cout << "==== TIC TAC TOE ====\n";
    while (true) {
        displayBoard();
        cout << "Player " << currentPlayer << " [" << currentMark << "] - Enter position (1-9): ";
        if (!(cin >> choice)) {
            cin.clear();
            cin.ignore(10000, '\n');
            cout << "Invalid input. Enter a number 1-9.\n";
            continue;
        }
        if (!markBoard(choice)) {
            cout << "Invalid move or box already filled! Try again.\n";
            continue;
        }
        if (checkWin()) {
            displayBoard();
            cout << "Player " << currentPlayer << " Wins!\n";
            break;
        }
        if (checkDraw()) {
            displayBoard();
            cout << "Game Draw!\n";
            break;
        }
        currentPlayer = (currentPlayer == 1) ? 2 : 1;
        currentMark = (currentMark == 'X') ? 'O' : 'X';
    }
    return 0;
}
