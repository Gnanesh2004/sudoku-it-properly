Def solve_sudoku (board):
 # Base case: If there are no empty cells left, puzzle is solved
 empty_cell = find_empty_cell (board)
 If not empty_cell:
 return True

 # Unpack row and col from empty_cell tuple
 row, col = empty_cell

 # Try numbers 1 through 9
 for num in range(1, 10):
 if is_valid(board, row, col, num):
 # If valid, place the number
 board[row][col] = num

 # Recursively attempt to solve the rest of the board
 if solve_sudoku(board):
 return True

 # If recursion fails, backtrack
 board[row][col] = 0

 # If no number worked, return False (triggering backtracking)
 return False
def find_empty_cell(board):
 # Find the first empty cell (represented by 0)
 for i in range(9):
 for j in range(9):
 if board[i][j] == 0:
 return (i, j)
 return None
def is_valid(board, row, col, num):
 # Check if placing num at board[row][col] is valid
 # Check the row
 if num in board[row]:
 return False

 # Check the column
 for i in range(9):
 if board[i][col] == num:
 return False

 # Check the 3x3 box
 box_start_row, box_start_col = 3 * (row // 3), 3 * (col // 3)
 for i in range(box_start_row, box_start_row + 3):
 for j in range(box_start_col, box_start_col + 3):
 if board[i][j] == num:
 return False

 return True
# Example usage:
if _name_ == "_main_":
 board = [
 [5, 3, 0, 0, 7, 0, 0, 0, 0],
 [6, 0, 0, 1, 9, 5, 0, 0, 0],
 [0, 9, 8, 0, 0, 0, 0, 6, 0],
 [8, 0, 0, 0, 6, 0, 0, 0, 3],
 [4, 0, 0, 8, 0, 3, 0, 0, 1],
 [7, 0, 0, 0, 2, 0, 0, 0, 6],
 [0, 6, 0, 0, 0, 0, 2, 8, 0],
 [0, 0, 0, 4, 1, 9, 0, 0, 5],
 [0, 0, 0, 0, 8, 0, 0, 7, 9]
 ]

 if solve_sudoku(board):
 print("Sudoku Solved:")
 for row in board:
 print(row)
 else:
 print("No solution exists")
