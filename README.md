import random
import time
import os

# ASCII Art for Game Start and End
def print_ascii_art():
    os.system('cls' if os.name == 'nt' else 'clear')  # Clear the terminal
    print("  _____                  _____                  _____                  _____")
    print(" / ____|                / ____|                |  __ \                |  __ \")
    print("| (___  __ _ _ __ ___  | (___  __ _ _ __ ___  __| |__) |  __ _ _ __ ___  __| |__) |")
    print("|___ \ / _` | '_ ` _ \ |___ \ / _` | '_ ` _ \ / ___/ __/ _` | '_ ` _ \ / ___/ __/ _` |")
    print("|___| | (_| | | | | | | |___| | (_| | | | | | | | | (__| (_| | | | | | | | (__| (_| |")
    print("     \____\__,_|_| |_|_|      \____\__,_|_| |_|_| |_|\___|\__,_|_| |_|_| |_|\___|\__,_|")
    print("                                                                                      ")
    print("  Tic Tac Toe Game  ")
    print("_____________________")

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
    return player1_name, player2_name

# Get Player Names for Single-Player Mode
def get_player_for_single_player_mode():
    player_name = input("Enter Player Name: ")
    print(f"Player: {player_name} (X)")
    return player_name

# Function to Draw the Board
def draw_board(board):
    os.system('cls' if os.name == 'nt' else 'clear')  # Clear the terminal
    print("  {} | {} | {}".format(board[0], board[1], board[2]))
    print("---+---+---")
    print("  {} | {} | {}".format(board[3], board[4], board[5]))
    print("---+---+---")
    print("  {} | {} | {}".format(board[6], board[7], board[8]))

# Function to Check for Win Conditions
def check_win(board):
    win_conditions = [(0, 1, 2), (3, 4, 5), (6, 7, 8), (0, 3, 6), (1, 4, 7), (2, 5, 8), (0, 4, 8), (2, 4, 6)]
    for condition in win_conditions:
        if board[condition[0]] == board[condition[1]] == board[condition[2]]!= " ":
            return True
    return False

# Function to Check for Draw
def check_draw(board):
    return " " not in board

# Function to Handle Player Move
def handle_player_move(board, player_name):
    move = input(f"{player_name}, enter your move (1-9): ")
    if board[int(move) - 1] == " ":
        board[int(move) - 1] = "X" if player_name == "Player 1" else "O"
        return True
    else:
        print("Invalid move, try again.")
        return handle_player_move(board, player_name)

# Function to Handle AI Move
def handle_ai_move(board):
    empty_squares = [i for i, x in enumerate(board) if x == " "]
    move = random.choice(empty_squares)
    board[move] = "O"
    return True

# Function to Play 2-Player Mode
def play_2_player_mode():
    player1_name, player2_name = get_players_for_2_player_mode()
    board = [" "] * 9
    while True:
        draw_board(board)
        if not handle_player_move(board, player1_name):
            continue
        if check_win(board):
            draw_board(board)
            print(f"Player 1 ({player1_name}) wins!")
            break
        if check_draw(board):
            draw_board(board)
            print("It's a draw!")
            break
        if not handle_player_move(board, player2_name):
            continue
        if check_win(board):
            draw_board(board)
            print(f"Player 2 ({player2_name}) wins!")
            break
        if check_draw(board):
            draw_board(board)
            print("It's a draw!")
            break

# Function to Play Single-Player Mode
def play_single_player_mode():
    player_name = get_player_for_single_player_mode()
    board = [" "] * 9
    while True:
        draw_board(board)
        if not handle_player_move(board, player_name):
            continue
        if check_win(board):
            draw_board(board)
            print(f"Player wins!")
            break
        if check_draw(board):
            draw_board(board)
            print("It's a draw!")
            break
        if not handle_ai_move(board):
            continue
        if check_win(board):
            draw_board(board)
            print("AI wins!")
            break
        if check_draw(board):
            draw_board(board)
            print("It's a draw!")
            break

# Function to Play 2-Player Mode with Sound Effects
def play_2_player_mode_with_sound():
    player1_name, player2_name = get_players_for_2_player_mode()
    board = [" "] * 9
    while True:
        draw_board(board)
        if not handle_player_move(board, player1_name):
            continue
        if check_win(board):
            draw_board(board)
            print(f"\a\a Player 1 ({player1_name}) wins!\a\a")
            break
        if check_draw(board):
            draw_board(board)
            print("\a\a It's a draw!\a\a")
            break
        if not handle_player_move(board, player2_name):
            continue
        if check_win(board):
            draw_board(board)
            print(f"\a\a Player 2 ({player2_name}) wins!\a\a")
            break
        if check_draw(board):
            draw_board(board)
            print("\a\a It's a draw!\a\a")
            break

# Main Game Function
def main_game():
    print_ascii_art()
    while True:
        print("\n1. 2-Player Mode")
        print("2. Single-Player Mode")
        print("3. Quit")
        choice = input("Enter your choice: ")
        if choice == "1":
            play_2_player_mode()
        elif choice == "2":
            play_single_player_mode()
        elif choice == "3":
            print("Thanks for playing!")
            break
        else:
            print("Invalid choice, try again.")

# Easter Egg: Type 'joke' to see a funny joke
def easter_egg():
    while True:
        joke = input("Want to hear a joke? Type 'joke' to hear one, or just press Enter to continue: ")
        if joke.lower() == "joke":
            print("Why couldn't the bicycle stand up by itself?")
            time.sleep(1)
            print("Because it was two-tired!")
            print("Ha ha, get it? Two-tired? Like a bicycle tire? Ahh, never mind...")
        else:
            break

# Main Program Loop
if __name__ == "__main__":
    main_game()
