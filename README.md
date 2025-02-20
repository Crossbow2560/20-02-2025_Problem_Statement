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

## Output Format
A two dimensional array consisting of the digits `1-4`.

## Example
### Input
![image](https://github.com/user-attachments/assets/a71829fd-9492-454d-84b0-5a3257e76636)=120x120
The input corresponding to the above board is:
> Input: board = [['.', '.', '.', '3'], ['.', '4', '.', '.'], ['1', '.', '.', '4'], ['.', '.', '3', '.']]

### Output
![image](https://github.com/user-attachments/assets/1da70e00-7386-4aa1-969f-76a72200d473)=120x120
The output corresponding to the above board is:
> Output: ans = [['2', '1', '4', '3'], ['3', '4', '1', '2'], ['1', '3', '2', '4'], ['4', '2', '3', '1']]


