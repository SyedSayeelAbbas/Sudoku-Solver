# Sudoku-Solver
This program is a Sudoku Solver implemented in C++. It solves a partially filled Sudoku grid using a backtracking algorithm and prints both the initial and the solved grid. Here's a detailed explanation:


---

Code Breakdown

1. Header Files

#include <iostream>
#include <vector>

<iostream>: Used for input/output operations (cout, cin).

<vector>: Utilized to store the possible numbers that can be placed in a cell.



---

2. Function: printSudoku

void printSudoku(int arr[9][9]) {
    cout<<"----------------------" << endl;
    for (int r = 0; r < 9; r++) {
        for (int c = 0; c < 9; c++) {
            cout<<arr[r][c] << " ";
        }
        cout<<endl;
    }
    cout<<"----------------------" << endl;
}

Prints the Sudoku grid in a formatted style.

Displays a separator before and after the grid.



---

3. Function: canPlace

bool canPlace(int arr[9][9], int row, int col, int n) {

Purpose: Determines if the number n can be placed in the cell (row, col) without violating Sudoku rules.


Logic:

1. Check Row:

for (int i = 0; i < 9; i++) {
    if (arr[row][i] == n) return false;
}

Ensures n does not already exist in the same row.


2. Check Column:

for (int i = 0; i < 9; i++) {
    if (arr[i][col] == n) return false;
}

Ensures n does not already exist in the same column.


3. Check 3x3 Subgrid:

int startRow = (row / 3) * 3;
int startCol = (col / 3) * 3;
for (int i = 0; i < 3; i++) {
    for (int j = 0; j < 3; j++) {
        if (arr[startRow + i][startCol + j] == n) return false;
    }
}

Ensures n does not exist in the corresponding 3x3 subgrid.




---

4. Function: findPlaceble

vector<int> findPlaceble(int arr[9][9], int r, int c) {

Purpose: Finds all numbers that can be legally placed in the cell (r, c).

Iterates through numbers 1-9, using canPlace to check validity, and stores valid numbers in a vector.



---

5. Function: findNextEmptyCell

bool findNextEmptyCell(int arr[9][9], int &row, int &col) {

Purpose: Finds the next empty cell in the grid (denoted by 0).

Logic:

Iterates through each cell in the grid.

If it finds a cell with value 0, it updates row and col and returns true.

If no empty cell is found, returns false (the Sudoku is solved).




---

6. Function: solveSudoku

bool solveSudoku(int arr[9][9]) {

Purpose: Solves the Sudoku grid using a recursive backtracking algorithm.


Logic:

1. Base Case:

if (!findNextEmptyCell(arr, row, col)) return true;

If no empty cells are left, the puzzle is solved.


2. Recursive Case:

vector<int> placeables = findPlaceble(arr, row, col);
for (int n : placeables) {
    arr[row][col] = n;
    if (solveSudoku(arr)) return true; // Recursively solve the rest of the grid.
    arr[row][col] = 0; // Backtrack if the solution fails.
}
return false;

Finds all valid numbers for the current cell.

Tries each number recursively.

If a number leads to a dead end, it resets the cell to 0 (backtracking).





---

7. Main Function

int main() {
    int board[9][9] = {
        {5, 3, 0, 0, 7, 0, 0, 0, 0},
        {6, 0, 0, 1, 9, 5, 0, 0, 0},
        {0, 9, 8, 0, 0, 0, 0, 6, 0},
        {8, 0, 0, 0, 6, 0, 0, 0, 3},
        {4, 0, 0, 8, 0, 3, 0, 0, 1},
        {7, 0, 0, 0, 2, 0, 0, 0, 6},
        {0, 6, 0, 0, 0, 0, 2, 8, 0},
        {0, 0, 0, 4, 1, 9, 0, 0, 0},
        {0, 0, 0, 0, 8, 0, 0, 7, 9}
    };
    printSudoku(board);
    if (solveSudoku(board)) {
        cout<<"Sudoku solved!"<<endl;
        printSudoku(board);
    } else {
        cout<<"No solution found."<<endl;
    }
    return 0;
}

Initializes a partially filled 9x9 Sudoku grid.

Prints the initial grid.

Calls solveSudoku to solve the grid.

If solvable, prints the solved grid; otherwise, prints "No solution found."



---

Example Run

Input Grid:

5 3 0 0 7 0 0 0 0
6 0 0 1 9 5 0 0 0
0 9 8 0 0 0 0 6 0
8 0 0 0 6 0 0 0 3
4 0 0 8 0 3 0 0 1
7 0 0 0 2 0 0 0 6
0 6 0 0 0 0 2 8 0
0 0 0 4 1 9 0 0 0
0 0 0 0 8 0 0 7 9

Output Grid:

5 3 4 6 7 8 9 1 2
6 7 2 1 9 5 3 4 8
1 9 8 3 4 2 5 6 7
8 5 9 7 6 1 4 2 3
4 2 6 8 5 3 7 9 1
7 1 3 9 2 4 8 5 6
9 6 1 5 3 7 2 8 4
2 8 7 4 1 9 6 3 5
3 4 5 2 8 6 1 7 9


---

Key Features

1. Backtracking Algorithm: Efficiently solves the puzzle by exploring all possible solutions.


2. Validation Functions: Ensures that all Sudoku rules are followed.


3. Readable Output: Prints the Sudoku grid in an intuitive format.



This is a simple yet powerful implementation of a Sudoku solver in C++.

