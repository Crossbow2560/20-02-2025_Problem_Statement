# 4x4 Sudoku Solver
## Problem Statement
Write a Program that can solve a 4x4 Sudoku by filling in the cells
The sudoku solution **must follow all the following rules**:
1. Each of the digits `1-4` must occur exactly once in each row.
2. Each of the digits `1-4` must occur exactly once in each column.
3. Each of the digits `1-4` must occur exactly once in each of the 4 `2x2` sub-boxes of the grid.

The `'.'` character indicates empty cells

## Input Format
A two dimensional array consisting of either digits `1-4` or the character `'.'`.

## Constraints
- `board.length == 4`
- `board[i].length == 4`
- `board[i][j]` is a digit `1-4` or a `'.'`.

## Output Format
A two dimensional array consisting of the digits `1-4`.

## Example
### Input
<img src="https://github.com/user-attachments/assets/a71829fd-9492-454d-84b0-5a3257e76636" width="300" height="300"/>

The input corresponding to the above board is:
> **Input**: board = [['.', '.', '.', '3'], ['.', '4', '.', '.'], ['1', '.', '.', '4'], ['.', '.', '3', '.']]

### Output
<img src="https://github.com/user-attachments/assets/1da70e00-7386-4aa1-969f-76a72200d473" width="300" height="300"/>

The output corresponding to the above board is:
> **Output**: ans = [['2', '1', '4', '3'], ['3', '4', '1', '2'], ['1', '3', '2', '4'], ['4', '2', '3', '1']]

## Test Cases
### **Input:**
```
board = [['.', '.', '.', '3'],['.', '4', '.', '.'], ['.', '.', '3', '2'], ['.', '.', '.', '.']]
```
### **Output:**
```
ans = [['1', '2', '4', '3'], ['3', '4', '2', '1'], ['4', '1', '3', '2'], ['2', '3', '1', '4']]
```
***
### **Input**
```
board = [['.', '.', '1', '.'],['.', '2', '.', '.'], ['.', '.', '2', '.'], ['.', '3', '.', '.']]
```
### **Output:**
```
ans = [['3', '4', '1', '2'], ['1', '2', '3', '4'], ['4', '1', '2', '3'], ['2', '3', '4', '1']]
```
***
### **Input**
```
board = [['.', '.', '.', '2'],['1', '.', '.', '.'], ['.', '.', '.', '1'], ['4', '.', '.', '.']]
```
### **Output:**
```
ans = [['3', '4', '1', '2'], ['1', '2', '3', '4'], ['2', '3', '4', '1'], ['4', '1', '2', '3']]
```
***
### **Input**
```
board = [['1', '3', '.', '.'],['.', '.', '.', '.'], ['.', '.', '.', '.'], ['.', '.', '1', '2']]
```
### **Output:**
```
ans = [['1', '3', '2', '4'],['4', '2', '3', '1'], ['2', '1', '4', '3'], ['3', '4', '1', '2']]
```
***
### **Input**
```
board = [['.', '3', '.', '.'],['2', '1', '.', '.'], ['.', '.', '1', '2'], ['.', '.', '3', '.']]
```
### **Output:**
```
ans = [['4', '3', '2', '1'],['2', '1', '4', '3'], ['3', '4', '1', '2'], ['1', '2', '3', '4']]
```
***
## Solution
Pseudocode:
```
FUNCTION is_valid(board, row, col, num):
    CONVERT num to STRING

    // Check if num is already in the row or column
    IF num exists in board[row] OR num exists in column board[i][col] for i in range(4):
        RETURN False

    // Check 2×2 sub-grid constraints
    SET start_row = (row // 2) * 2
    SET start_col = (col // 2) * 2
    FOR each cell (r, c) in the 2×2 sub-grid:
        IF board[r][c] == num:
            RETURN False

    RETURN True  // Number placement is valid

FUNCTION solve_sudoku(board):
    FOR each row in range(4):
        FOR each col in range(4):
            IF board[row][col] is empty ('.'):  // Find the first empty cell
                FOR each num in ['1', '2', '3', '4']:  // Try numbers 1 to 4
                    IF is_valid(board, row, col, num):
                        PLACE num in board[row][col]
                        IF solve_sudoku(board):  // Recursively attempt solving
                            RETURN True
                        RESET board[row][col] to '.'  // Undo move (backtrack)
                RETURN False  // No valid number found, backtrack
    RETURN True  // Sudoku solved successfully

FUNCTION print_board(board):
    FOR each row in board:
        PRINT row as a space-separated string

// Example input board
INITIALIZE board as a 4×4 grid with '.' representing empty cells

IF solve_sudoku(board):
    PRINT "Solved Sudoku:"
    CALL print_board(board)
ELSE:
    PRINT "No solution exists."
```

***
## Implementation
```python
def is_valid(board, row, col, num):
    """Check if placing num in board[row][col] is valid."""
    num = str(num)
    
    # Check row and column constraints
    if num in board[row] or num in [board[i][col] for i in range(4)]:
        return False
    
    # Check 2x2 sub-grid constraints
    start_row, start_col = (row // 2) * 2, (col // 2) * 2
    sub_grid = [board[r][c] for r in range(start_row, start_row + 2) for c in range(start_col, start_col + 2)]
    if num in sub_grid:
        return False
    
    return True

def solve_sudoku(board):
    """Solve the 4x4 Sudoku using backtracking."""
    for row in range(4):
        for col in range(4):
            if board[row][col] == '.':  # Find the first empty cell
                for num in '1234':  # Try numbers 1 to 4
                    if is_valid(board, row, col, num):
                        board[row][col] = num  # Place number
                        if solve_sudoku(board):  # Recursively solve
                            return True
                        board[row][col] = '.'  # Undo move (backtrack)
                return False  # No valid number found
    return True  # Solved successfully

def print_board(board):
    """Prints the Sudoku board in a readable format."""
    for row in board:
        print(" ".join(row))

# Example input board
board = [['.', '.', '.', '3'], 
         ['.', '4', '.', '.'], 
         ['1', '.', '.', '4'], 
         ['.', '.', '3', '.']]

# Solve the Sudoku and print the result
if solve_sudoku(board):
    print("Solved Sudoku:")
    print_board(board)
else:
    print("No solution exists.")
```
