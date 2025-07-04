import copy

def solve_sudoku(board):
    find = find_empty(board)
    if not find:
        return True
    else:
        row, col = find

    for i in range(1, 10):
        if is_valid(board, i, (row, col)):
            board[row][col] = i

            if solve_sudoku(board):
                return True
            
            board[row][col] = 0

    return False

def find_empty(board):
    for r in range(9):
        for c in range(9):
            if board[r][c] == 0:
                return (r, c)
    return None

def is_valid(board, num, pos):
    row, col = pos

    for c in range(9):
        if board[row][c] == num and col != c:
            return False

    for r in range(9):
        if board[r][col] == num and row != r:
            return False

    box_x = col // 3
    box_y = row // 3

    for r in range(box_y * 3, box_y * 3 + 3):
        for c in range(box_x * 3, box_x * 3 + 3):
            if board[r][c] == num and (r, c) != pos:
                return False

    return True

def print_board(board):
    for r in range(9):
        if r % 3 == 0 and r != 0:
            print("- - - - - - - - - - - - ")

        for c in range(9):
            if c % 3 == 0 and c != 0:
                print(" | ", end="")

            if c == 8:
                print(board[r][c])
            else:
                print(str(board[r][c]) + " ", end="")

