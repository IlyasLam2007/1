import random
import time
import os

# ASCII Art for Game Start and End
def print_ascii_art():
    os.system('cls' if os.name == 'nt' else 'clear')  # Clear the terminal
    print("=====================================")
    print("             Bonjourno!              ")
    print("=====================================\n")
    print("Welcome to the Ultimate Tic Tac Toe!\n")

# Customizable Player Names
def get_player_names():
    player1_name = input("Enter Player 1 Name: ")
    player2_name = input("Enter Player 2 Name: ")
    return player1_name, player2_name

# Get Player Names for 2-Player Mode
def get_players_for_2_player_mode():
    player1_name, player2_name = get_player_names()
    print(f"Player 1: {player1_name} (X)")
    print(f"Player 2: {player2_name} (O)")
    return {
        'player1': {'name': player1_name, 'marker': 'X'},
        'player2': {'name': player2_name, 'marker': 'O'}
    }

# Get Player Name for Single Player
def get_player_for_single_player_mode():
    player_name = input("Enter Player Name: ")
    print(f"Player: {player_name} (X)")
    return {'name': player_name, 'marker': 'X'}

# Function to Draw the Board
def draw_board(board):
    os.system('cls' if os.name == 'nt' else 'clear')  # Clear the terminal
    print("\n")
    print(f" {board[0]} | {board[1]} | {board[2]} ")
    print("---+---+---")
    print(f" {board[3]} | {board[4]} | {board[5]} ")
    print("---+---+---")
    print(f" {board[6]} | {board[7]} | {board[8]} ")
    print("\n")

# Function to Check for Win Conditions
def check_win(board):
    win_conditions = [
        (0, 1, 2), (3, 4, 5), (6, 7, 8),
        (0, 3, 6), (1, 4, 7), (2, 5, 8),
        (0, 4, 8), (2, 4, 6)
    ]
    for condition in win_conditions:
        if board[condition[0]] == board[condition[1]] == board[condition[2]] != " ":
            return True
    return False

# Function to Check for Draw
def check_draw(board):
    return " " not in board

# Handle Player Move with marker parameter
def handle_player_move(board, player):
    move = input(f"{player['name']} ({player['marker']}), enter your move (1-9): ")
    if move in [str(i) for i in range(1, 10)]:
        index = int(move) - 1
        if board[index] == " ":
            board[index] = player['marker']
            return True
        else:
            print("That spot is already taken. Try again.")
            return handle_player_move(board, player)
    else:
        print("Invalid input. Please enter a number from 1 to 9.")
        return handle_player_move(board, player)

# Handle AI Move with marker parameter
def handle_ai_move(board, marker):
    empty_squares = [i for i, x in enumerate(board) if x == " "]
    move = random.choice(empty_squares)
    board[move] = marker
    print("Tabby is making a move...")
    time.sleep(1)
    return True

# Function to Play 2-Player Mode
def play_2_player_mode():
    players = get_players_for_2_player_mode()
    board = [" "] * 9
    current_player = players['player1']
    while True:
        draw_board(board)
        handle_player_move(board, current_player)
        if check_win(board):
            draw_board(board)
            print(f" {current_player['name']} wins and gets all the honour! \n")
            break
        if check_draw(board):
            draw_board(board)
            print("It's a draw! WHAT A LETDOWN \n")
            break
        # Switch players
        current_player = players['player2'] if current_player == players['player1'] else players['player1']

# Function to Play Single-Player Mode
def play_single_player_mode():
    player = get_player_for_single_player_mode()
    board = [" "] * 9
    while True:
        draw_board(board)
        handle_player_move(board, player)
        if check_win(board):
            draw_board(board)
            print(f" {player['name']} wins! Congratulations for uhh beating a cat... i hope it inflates your ego MONSTER! \n")
            break
        if check_draw(board):
            draw_board(board)
            print("It's a draw! \n")
            break
        handle_ai_move(board, 'O')  # AI marker is 'O'
        if check_win(board):
            draw_board(board)
            print("Tabby wins! YOU GOT OUSMARTED BY A CAT LLLLLL!!! Better luck next time bastard! \n")
            break
        if check_draw(board):
            draw_board(board)
            print("It's a draw! DISSAPOINTING \n")
            break

# Main Game Function
def main_game():
    print_ascii_art()
    while True:
        print("Choose Mode:")
        print("1. 2-Player Mode")
        print("2. Single-Player Mode")
        print("3. Quit")
        choice = input("Enter your choice: ")
        if choice == "1":
            play_2_player_mode()
        elif choice == "2":
            play_single_player_mode()
        elif choice == "3":
            print("So soon? Lazy Pig... Thanks for playing! Come back soon!")
            break
        else:
            print("Invalid choice, try again.")

# Easter Egg: Joke feature
def easter_egg():
    while True:
        joke = input("Want to hear a joke? Type 'joke' or press Enter to skip: ")
        if joke.lower() == "joke":
            print("Why did the scarecrow win an award? Because he was outstanding in his field! ")
        else:
            break

# Run the game
if __name__ == "__main__":
    main_game()
