import sys

def print_board(board):
    """
    Prints the current state of the game board.
    """
    print("\n")
    print(f" {board[0][0]} | {board[0][1]} | {board[0][2]} ")
    print("---|---|---")
    print(f" {board[1][0]} | {board[1][1]} | {board[1][2]} ")
    print("---|---|---")
    print(f" {board[2][0]} | {board[2][1]} | {board[2][2]} ")
    print("\n")

def check_winner(board, player):
    """
    Checks if the current player has won the game.
    """
    # Check rows
    for row in board:
        if all([cell == player for cell in row]):
            return True
    
    # Check columns
    for col in range(3):
        if all([board[row][col] == player for row in range(3)]):
            return True
    
    # Check diagonals
    if all([board[i][i] == player for i in range(3)]):
        return True
    if all([board[i][2 - i] == player for i in range(3)]):
        return True
    
    return False

def check_draw(board):
    """
    Checks if the game is a draw (no empty spaces left).
    """
    for row in board:
        if any([cell == ' ' for cell in row]):
            return False
    return True

def get_player_move(board, player):
    """
    Prompts the current player to make a move.
    Validates input.
    """
    while True:
        try:
            move = input(f"Player {player}, enter your move as row and column (e.g., 1 3 for row 1, column 3): ")
            row_str, col_str = move.strip().split()
            row, col = int(row_str) - 1, int(col_str) - 1
            
            if row not in range(3) or col not in range(3):
                print("Invalid input. Row and column must be between 1 and 3. Please try again.")
                continue
            
            if board[row][col] != ' ':
                print("This cell is already occupied. Please choose another one.")
                continue
            
            return row, col
        except ValueError:
            print("Invalid input format. Please enter two numbers separated by a space (e.g., 2 3).")

def play_game():
    """
    Main function to control the game flow.
    """
    print("Welcome to Tic Tac Toe!")
    while True:
        # Initialize the game board
        board = [[' ' for _ in range(3)] for _ in range(3)]
        current_player = 'X'
        game_over = False
        
        while not game_over:
            print_board(board)
            row, col = get_player_move(board, current_player)
            board[row][col] = current_player
            
            # Check for win
            if check_winner(board, current_player):
                print_board(board)
                print(f"Congratulations! Player {current_player} wins!\n")
                game_over = True
            # Check for draw
            elif check_draw(board):
                print_board(board)
                print("It's a draw!\n")
                game_over = True
            else:
                # Switch players
                current_player = 'O' if current_player == 'X' else 'X'
        
        # Replay option
        replay = input("Do you want to play again? (y/n): ").lower()
        if replay != 'y':
            print("Thanks for playing Tic Tac Toe! Goodbye!")
            break

if __name__ == "__main__":
    play_game()
