from IPython.display import clear_output

def display_board(board):
    clear_output()
    print(board[1]+'|', board[2]+'|' ,board[3])
    print('------------')
    print(board[4]+'|', board[5]+'|', board[6])
    print('------------')
    print(board[7]+'|',board[8]+'|', board[9])
  
test_board = ['#','X','O','X','O','X','O','X','O','X']
display_board(test_board)
def player_input():
    mark=''
    # while mark != 'X' and mark != "O":
    #     mark=(input("Player1 enters 'X' or 'O'").upper())

    # player1=mark
    # if player1 == 'X':
    #     player2='O'
    # else :
    #     player2='X'
    # return (player1,player2)
    while not (mark == 'X' or mark == 'O'):
        mark = (input("Player1 : as 'X' or 'O' is ").upper())

    if mark =='X':
        return ('X','O')
    else:
        return('O','X')

player1_mark , player2_mark = player_input()
def place_marker(board, mark, position):
        board[position]=mark
def win_check(board, mark):
    return ((board[9]== mark and board[8]== mark and board[7]== mark)or 
            (board[4]== mark and board[5]== mark and board[6]== mark)or
            (board[1]== mark and board[2]== mark and board[3]== mark)or
            (board[7]== mark and board[4]== mark and board[1]== mark)or
            (board[8]== mark and board[5]== mark and board[2]== mark)or
            (board[9]== mark and board[6]== mark and board[3]== mark)or
            (board[9]== mark and board[5]== mark and board[1]== mark)or
            (board[7]== mark and board[5]== mark and board[3]== mark))
import random

def choose_first():
    flip= random.randint(0,1)

    if flip==0:
        return 'Player 1'
    else :
        return 'Player 2'
def space_check(board, position):
    
    return board[position] == ''
def full_board_check(board):
    for i in range (1,10):
        if space_check(board,i):
            return False
    return True
def player_choice(board):
    position = 0
    while position not in [1,2,3,4,5,6,7,8,9] or not space_check(board,position):
        position = int(input("Choose a Position 1-9"))

    return position
def replay():
    choice= input("Do you want to play again? type Yes or NO")
    
    return choice == 'Yes'
print('Welcome to Tic Tac Toe!')

while True:
    the_board=['']*10
    player1_mark,player2_mark=player_input()
    turn = choose_first()
    print(turn+ 'will go first')

    play_game = input("Ready to play ? Y or N")
    if play_game == 'Y':
        game_on = True
    elif play_game == 'N':
        game_on=False 

    while game_on:
        if turn == 'Player 1':
            display_board(the_board)
            position = player_choice(the_board)
            place_marker(the_board,player1_mark,position)
            if win_check(the_board,player1_mark):
                display_board(the_board)
                print('Player 1 has won!')
                game_on=False
            else:
                if full_board_check(the_board):
                    display_board(the_board)
                    print('TIE!')
                    game_on=False
                else:
                    turn= 'Player 2'
        else:
            display_board(the_board)
            position = player_choice(the_board)
            place_marker(the_board,player2_mark,position)
            if win_check(the_board,player2_mark):
                display_board(the_board)
                print('Player 2 has won!')
                game_on=False
            else:
                if full_board_check(the_board):
                    display_board(the_board)
                    print('TIE!')
                    game_on=False
                else:
                    turn= 'Player 1'
            
    if not replay():
        break
         
        



         
