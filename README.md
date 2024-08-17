# tic-tac-toi-game-
//1st part




import tkinter as tk
from tkinter import messagebox

class TicTacToe:
    def __init__(self, master):
        self.master = master
        self.master.title("Tic Tac Toe")
        self.board = [[' ' for _ in range(3)] for _ in range(3)]
        self.current_player = 'X'
        self.buttons = [[None]*3 for _ in range(3)]
        self.create_widgets()
        self.player_X_score = 0
        self.player_O_score = 0

    def create_widgets(self):
        self.scoreboard = tk.Label(self.master, text="Scoreboard: X - 0, O - 0", font=('Helvetica', 12))
        self.scoreboard.grid(row=0, column=0, columnspan=3)

        for i in range(3):
            for j in range(3):
                self.buttons[i][j] = tk.Button(self.master, text='', font=('Helvetica', 20), width=5, height=2,
                                                command=lambda row=i, col=j: self.on_click(row, col))
                self.buttons[i][j].grid(row=i+1, column=j, padx=5, pady=5)

        self.reset_button = tk.Button(self.master, text="Reset", font=('Helvetica', 12), command=self.reset)
        self.reset_button.grid(row=4, column=1, columnspan=3, pady=10)

    def on_click(self, row, col):
        if self.board[row][col] == ' ':
            self.board[row][col] = self.current_player
            self.buttons[row][col].config(text=self.current_player, state='disabled', disabledforeground='black')

            if self.check_winner():
                self.update_scoreboard()
                messagebox.showinfo("Congratulations!", f"Player {self.current_player} wins!")
                self.reset()
            elif self.check_draw():
                messagebox.showinfo("Draw", "It's a draw!")
                self.reset()
            else:
                self.switch_player()

    def check_winner(self):
        # Check rows, columns, and diagonals for a winner
        for i in range(3):
            if self.board[i][0] == self.board[i][1] == self.board[i][2] != ' ':
                return True
            if self.board[0][i] == self.board[1][i] == self.board[2][i] != ' ':
                return True
        if self.board[0][0] == self.board[1][1] == self.board[2][2] != ' ':
            return True
        if self.board[0][2] == self.board[1][1] == self.board[2][0] != ' ':
            return True
        return False

    def check_draw(self):
        for row in self.board:
            for cell in row:
                if cell == ' ':
                    return False
        return True

    def switch_player(self):
        self.current_player = 'O' if self.current_player == 'X' else 'X'

    def reset(self):
        for i in range(3):
            for j in range(3):
                self.buttons[i][j].config(text='', state='normal')
                self.board[i][j] = ' '
        self.current_player = 'X'

    def update_scoreboard(self):
        if self.current_player == 'X':
            self.player_X_score += 1
        else:
            self.player_O_score += 1
        self.scoreboard.config(text=f"Scoreboard: X - {self.player_X_score}, O - {self.player_O_score}")


if __name__ == "__main__":
    root = tk.Tk()
    game = TicTacToe(root)
    root.mainloop()


//2nd part


import tkinter as tk
import tkinter.messagebox


window=tk.Tk()
window.title('Tic Tac Toe')
frame=tk.Frame(master=window)
window.configure(bg='#8ca6fa')
frame.pack(pady=10)

label=tk.Label(master=frame,text="TIC TAC TOE",font=("Arial", 20, 'bold'), bg='#8ca6fa')
label.pack()

frame1=tk.Frame(master=window,borderwidth=2,relief=tk.SUNKEN,bg='#fad82d')
frame1.pack(padx=10,pady=10)

button1=tk.Button(master=frame1,text='',width=10,height=5,bg='#92f7be',command=lambda : buttonclick(1))
button1.grid(row=0,column=0,padx=5,pady=5)

button2=tk.Button(master=frame1,text='',width=10,height=5,bg='#92f7be',command=lambda : buttonclick(2))
button2.grid(row=0,column=1,padx=5,pady=5)

button3=tk.Button(master=frame1,text='',width=10,height=5,bg='#92f7be',command=lambda : buttonclick(3))
button3.grid(row=0,column=2,padx=5,pady=5)

button4=tk.Button(master=frame1,text='',width=10,height=5,bg='#92f7be',command=lambda : buttonclick(4))
button4.grid(row=1,column=0,padx=5,pady=5)

button5=tk.Button(master=frame1,text='',width=10,height=5,bg='#92f7be',command=lambda : buttonclick(5))
button5.grid(row=1,column=1,padx=5,pady=5)

button6=tk.Button(master=frame1,text='',width=10,height=5,bg='#92f7be',command=lambda : buttonclick(6))
button6.grid(row=1,column=2,padx=5,pady=5)

button7=tk.Button(master=frame1,text='',width=10,height=5,bg='#92f7be',command=lambda : buttonclick(7))
button7.grid(row=2,column=0,padx=5,pady=5)

button8=tk.Button(master=frame1,text='',width=10,height=5,bg='#92f7be',command=lambda : buttonclick(8))
button8.grid(row=2,column=1,padx=5,pady=5)

button9=tk.Button(master=frame1,text='',width=10,height=5,bg='#92f7be',command=lambda : buttonclick(9))
button9.grid(row=2,column=2,padx=5,pady=5)

frame2=tk.Frame(master=window,border=2,relief=tk.SUNKEN,bg='#f2fac3')
frame2.pack()
label1=tk.Label(master=frame2,text="Player 1 --> X\nPlayer 2 --> O",width=10,bg='#f2fac3')
label1.grid(row=0,column=0,padx=5)
button_restart=tk.Button(master=frame2,text="Restart",width=10,height=3,bg='#eac3fa',relief=tk.GROOVE,command=lambda: restartbutton())
button_restart.grid(row=0,column=1,padx=10,pady=10)
label2=tk.Label(master=frame2,text='Player-1 Turn',bg="#42d104",width=10,height=3,relief=tk.SUNKEN)
label2.grid(row=0,column=2,padx=5)
a=1
b=0
c=0
player1_wins = 0
player2_wins = 0

def disablebutton():
    button1['state']=tk.DISABLED
    button2['state']=tk.DISABLED
    button3['state']=tk.DISABLED
    button4['state']=tk.DISABLED
    button5['state']=tk.DISABLED
    button6['state']=tk.DISABLED
    button7['state']=tk.DISABLED
    button8['state']=tk.DISABLED
    button9['state']=tk.DISABLED

def restartbutton():
    global a,b,c
    a=1
    b=0
    c=0
    label2['bg']="#42d104"
    label2['text']='Player-1 Turn'
    button1['text']=''
    button1['bg']='#92f7be'
    button2['text']=''
    button2['bg']='#92f7be'
    button3['text']=''
    button3['bg']='#92f7be'
    button4['text']=''
    button4['bg']='#92f7be'
    button5['text']=''
    button5['bg']='#92f7be'
    button6['text']=''
    button6['bg']='#92f7be'
    button7['text']=''
    button7['bg']='#92f7be'
    button8['text']=''
    button8['bg']='#92f7be'
    button9['text']=''
    button9['bg']='#92f7be'
    button1['state']=tk.NORMAL
    button2['state']=tk.NORMAL
    button3['state']=tk.NORMAL
    button4['state']=tk.NORMAL
    button5['state']=tk.NORMAL
    button6['state']=tk.NORMAL
    button7['state']=tk.NORMAL
    button8['state']=tk.NORMAL
    button9['state']=tk.NORMAL

def buttonclick(x):
    global a,b,c
    #for player 1
    if(x==1 and a==1 and button1['text']==''):
        button1['text']="X"
        button1['bg']="#42d104"
        label2['bg']="#e8956f"
        label2['text']='Player-2 Turn'
        a=0
        b+=1
    if(x==2 and a==1 and button2['text']==''):
        button2['text']="X"
        button2['bg']="#42d104"
        label2['bg']="#e8956f"
        label2['text']='Player-2 Turn'
        a=0
        b+=1
    if(x==3 and a==1 and button3['text']==''):
        button3['text']="X"
        button3['bg']="#42d104"
        label2['bg']="#e8956f"
        label2['text']='Player-2 Turn'
        a=0
        b+=1
    if(x==4 and a==1 and button4['text']==''):
        button4['text']="X"
        button4['bg']="#42d104"
        label2['bg']="#e8956f"
        label2['text']='Player-2 Turn'
        a=0
        b+=1
    if(x==5 and a==1 and button5['text']==''):
        button5['text']="X"
        button5['bg']="#42d104"
        label2['bg']="#e8956f"
        label2['text']='Player-2 Turn'
        a=0
        b+=1
    if(x==6 and a==1 and button6['text']==''):
        button6['text']="X"
        button6['bg']="#42d104"
        label2['bg']="#e8956f"
        label2['text']='Player-2 Turn'
        a=0
        b+=1
    if(x==7 and a==1 and button7['text']==''):
        button7['text']="X"
        button7['bg']="#42d104"
        label2['bg']="#e8956f"
        label2['text']='Player-2 Turn'
        a=0
        b+=1
    if(x==8 and a==1 and button8['text']==''):
        button8['text']="X"
        button8['bg']="#42d104"
        label2['bg']="#e8956f"
        label2['text']='Player-2 Turn'
        a=0
        b+=1
    if(x==9 and a==1 and button9['text']==''):
        button9['text']="X"
        button9['bg']="#42d104"
        label2['bg']="#e8956f"
        label2['text']='Player-2 Turn'
        a=0
        b+=1

    #for player 2
    if(x==1 and a==0 and button1['text']==''):
        button1['text']='O'
        button1['bg']="#e8956f"
        label2['bg']="#42d104"
        label2['text']='Player-1 Turn'
        a=1
        b+=1
    if(x==2 and a==0 and button2['text']==''):
        button2['text']='O'
        button2['bg']="#e8956f"
        label2['bg']="#42d104"
        label2['text']='Player-1 Turn'
        a=1
        b+=1
    if(x==3 and a==0 and button3['text']==''):
        button3['text']='O'
        button3['bg']="#e8956f"
        label2['bg']="#42d104"
        label2['text']='Player-1 Turn'
        a=1
        b+=1
    if(x==4 and a==0 and button4['text']==''):
        button4['text']='O'
        button4['bg']="#e8956f"
        label2['bg']="#42d104"
        label2['text']='Player-1 Turn'
        a=1
        b+=1
    if(x==5 and a==0 and button5['text']==''):
        button5['text']='O'
        button5['bg']="#e8956f"
        label2['bg']="#42d104"
        label2['text']='Player-1 Turn'
        a=1
        b+=1
    if(x==6 and a==0 and button6['text']==''):
        button6['text']='O'
        button6['bg']="#e8956f"
        label2['bg']="#42d104"
        label2['text']='Player-1 Turn'
        a=1
        b+=1
    if(x==7 and a==0 and button7['text']==''):
        button7['text']='O'
        button7['bg']="#e8956f"
        label2['bg']="#42d104"
        label2['text']='Player-1 Turn'
        a=1
        b+=1
    if(x==8 and a==0 and button8['text']==''):
        button8['text']='O'
        button8['bg']="#e8956f"
        label2['bg']="#42d104"
        label2['text']='Player-1 Turn'
        a=1
        b+=1
    if(x==9 and a==0 and button9['text']==''):
        button9['text']='O'
        button9['bg']="#e8956f"
        label2['bg']="#42d104"
        label2['text']='Player-1 Turn'
        a=1
        b+=1

    #checking winner
    if(button1['text']=='X' and button2['text']=='X' and button3['text']=='X' or
        button4['text']=='X' and button5['text']=='X' and button6['text']=='X' or
        button7['text']=='X' and button8['text']=='X' and button9['text']=='X' or
        button1['text']=='X' and button4['text']=='X' and button7['text']=='X' or
        button2['text']=='X' and button5['text']=='X' and button8['text']=='X' or
        button3['text']=='X' and button6['text']=='X' and button9['text']=='X' or
        button1['text']=='X' and button5['text']=='X' and button9['text']=='X' or
        button3['text']=='X' and button5['text']=='X' and button7['text']=='X'):
            disablebutton()
            c=1
            tkinter.messagebox.showinfo("Tic Tac Toe","Winner is player 1")
    elif( button1['text']=='O' and button2['text']=='O' and button3['text']=='O' or
        button4['text']=='O' and button5['text']=='O' and button6['text']=='O' or
        button7['text']=='O' and button8['text']=='O' and button9['text']=='O' or
        button1['text']=='O' and button4['text']=='O' and button7['text']=='O' or
        button2['text']=='O' and button5['text']=='O' and button8['text']=='O' or
        button3['text']=='O' and button6['text']=='O' and button9['text']=='O' or
        button1['text']=='O' and button5['text']=='O' and button9['text']=='O' or
        button3['text']=='O' and button5['text']=='O' and button7['text']=='O'):
            disablebutton()
            c=1
            tkinter.messagebox.showinfo("Tic Tac Toe","Winner is player 2")
    elif(b==9):
        disablebutton()
        c=1
        tkinter.messagebox.showinfo("Tic Tac Toe","Match is Draw.")

window.mainloop()



import tkinter as tk
from tkinter import messagebox

class TicTacToe:
    def __init__(self):
        self.window = tk.Tk()
        self.window.title('Tic Tac Toe')
        self.window.configure(bg='#8ca6fa')

        self.frame = tk.Frame(master=self.window)
        self.frame.pack(pady=10)

        self.label = tk.Label(master=self.frame, text="TIC TAC TOE", font=("Arial", 20, 'bold'), bg='#8ca6fa')
        self.label.pack()

        self.frame1 = tk.Frame(master=self.window, borderwidth=2, relief=tk.SUNKEN, bg='#d7fc03')
        self.frame1.pack(padx=10, pady=10)

        self.buttons = [[None for _ in range(3)] for _ in range(3)]
        for i in range(3):
            for j in range(3):
                self.buttons[i][j] = tk.Button(master=self.frame1, text='', width=10, height=5, bg='#92f7be',
                                                command=lambda row=i, col=j: self.button_click(row, col))
                self.buttons[i][j].grid(row=i, column=j, padx=5, pady=5)

        self.frame2 = tk.Frame(master=self.window, border=2, relief=tk.SUNKEN, bg='#f2fac3')
        self.frame2.pack()

        self.label1 = tk.Label(master=self.frame2, text="Player 1 --> X\nPlayer 2 --> O", width=10, bg='#f2fac3')
        self.label1.grid(row=0, column=0, padx=5)

        self.button_restart = tk.Button(master=self.frame2, text="Restart", width=10, height=3, bg='#eac3fa', relief=tk.GROOVE, command=self.restart)
        self.button_restart.grid(row=0, column=1, padx=10, pady=10)

        self.label2 = tk.Label(master=self.frame2, text='Player-1 Turn', bg="skyblue", width=10, height=3, relief=tk.SUNKEN)
        self.label2.grid(row=0, column=2, padx=5)

        self.scoreboard_frame = tk.Frame(master=self.window, border=2, relief=tk.SUNKEN, bg='#f2fac3')
        self.scoreboard_frame.pack(pady=10)

        self.player1_score = 0
        self.player2_score = 0

        self.player1_label = tk.Label(master=self.scoreboard_frame, text="Player 1 Score: ", bg='#f2fac3')
        self.player1_label.grid(row=0, column=0, padx=5, pady=5)

        self.player1_score_label = tk.Label(master=self.scoreboard_frame, text=str(self.player1_score), bg='#f2fac3')
        self.player1_score_label.grid(row=0, column=1, padx=5, pady=5)

        self.player2_label = tk.Label(master=self.scoreboard_frame, text="Player 2 Score: ", bg='#f2fac3')
        self.player2_label.grid(row=1, column=0, padx=5, pady=5)

        self.player2_score_label = tk.Label(master=self.scoreboard_frame, text=str(self.player2_score), bg='#f2fac3')
        self.player2_score_label.grid(row=1, column=1, padx=5, pady=5)

        self.current_player = "X"
        self.moves = 0
        self.game_over = False

    def button_click(self, row, col):
        if not self.game_over and self.buttons[row][col]["text"] == "":
            self.buttons[row][col]["text"] = self.current_player
            self.moves += 1
            if self.check_winner():
                self.update_scoreboard()
                messagebox.showinfo("Congratulations!", f"Player {self.current_player} wins!")
                self.game_over = True
            elif self.moves == 9:
                messagebox.showinfo("Tie!", "The game is a tie!")
                self.game_over = True
            else:
                self.toggle_player()

    def toggle_player(self):
        self.current_player = "O" if self.current_player == "X" else "X"
        self.label2.config(text=f"Player-{self.current_player} Turn")

    def check_winner(self):
        board = [[self.buttons[i][j]["text"] for j in range(3)] for i in range(3)]
        for i in range(3):
            if board[i][0] == board[i][1] == board[i][2] != "":
                return True
            if board[0][i] == board[1][i] == board[2][i] != "":
                return True
        if board[0][0] == board[1][1] == board[2][2] != "":
            return True
        if board[0][2] == board[1][1] == board[2][0] != "":
            return True
        return False

    def update_scoreboard(self):
        if self.current_player == "X":
            self.player1_score += 1
            self.player1_score_label.config(text=str(self.player1_score))
        else:
            self.player2_score += 1
            self.player2_score_label.config(text=str(self.player2_score))

    def restart(self):
        for i in range(3):
            for j in range(3):
                self.buttons[i][j].config(text="")
        self.current_player = "X"
        self.moves = 0
        self.game_over = False
        self.label2.config(text='Player-1 Turn')

    def run(self):
        self.window.mainloop()

if __name__ == "__main__":
    game = TicTacToe()
    game.run()




//3rd part




from tkinter import *
import numpy as np

size_of_board = 600
symbol_size = (size_of_board / 3 - size_of_board / 8) / 2
symbol_thickness = 50
symbol_X_color = '#EE4035'
symbol_O_color = '#0492CF'
Green_color = '#7BC043'
Blue_color = '#8EE5EE'

class Tic_Tac_Toe():
    def __init__(self):
        self.window = Tk()
        self.window.title('Tic-Tac-Toe')
        self.canvas = Canvas(self.window, width=size_of_board, height=size_of_board, background=Blue_color)
        self.canvas.pack()
        self.window.bind('<Button-1>', self.click)

        self.initialize_board()
        self.player_X_turns = True
        self.board_status = np.zeros(shape=(3, 3))

        self.player_X_starts = True
        self.reset_board = False
        self.gameover = False
        self.tie = False
        self.X_wins = False
        self.O_wins = False

        self.X_score = 0
        self.O_score = 0
        self.tie_score = 0

    def mainloop(self):
        self.window.mainloop()

    def initialize_board(self):
        for i in range(2):
            self.canvas.create_line((i + 1) * size_of_board / 3, 0, (i + 1) * size_of_board / 3, size_of_board)

        for i in range(2):
            self.canvas.create_line(0, (i + 1) * size_of_board / 3, size_of_board, (i + 1) * size_of_board / 3)

    def play_again(self):
        self.initialize_board()
        self.player_X_starts = not self.player_X_starts
        self.player_X_turns = self.player_X_starts
        self.board_status = np.zeros(shape=(3, 3))

    def draw_O(self, logical_position):
        logical_position = np.array(logical_position)

        grid_position = self.convert_logical_to_grid_position(logical_position)
        self.canvas.create_oval(grid_position[0] - symbol_size, grid_position[1] - symbol_size,
                                grid_position[0] + symbol_size, grid_position[1] + symbol_size, width=symbol_thickness,
                                outline=symbol_O_color)

    def draw_X(self, logical_position):
        grid_position = self.convert_logical_to_grid_position(logical_position)
        self.canvas.create_line(grid_position[0] - symbol_size, grid_position[1] - symbol_size,
                                grid_position[0] + symbol_size, grid_position[1] + symbol_size, width=symbol_thickness,
                                fill=symbol_X_color)
        self.canvas.create_line(grid_position[0] - symbol_size, grid_position[1] + symbol_size,
                                grid_position[0] + symbol_size, grid_position[1] - symbol_size, width=symbol_thickness,
                                fill=symbol_X_color)

    def display_gameover(self):

        if self.X_wins:
            self.X_score += 1
            text = '  : WINNER : \n  Player 1 (X) \n--------------------'
            color = symbol_X_color
        elif self.O_wins:
            self.O_score += 1
            text = '  : WINNER : \n  Player 2 (O) \n--------------------'
            color = symbol_O_color
        else:
            self.tie_score += 1
            text = 'Its a tie'
            color = 'gray'

        self.canvas.delete("all")
        self.canvas.create_text(size_of_board / 2, size_of_board / 3, font="cmr 60 bold", fill=color, text=text)

        score_text = 'Scores \n'
        self.canvas.create_text(size_of_board / 2, 5 * size_of_board / 8, font="cmr 40 bold", fill=Green_color,
                                text=score_text)

        score_text = 'Player 1 (X) : ' + str(self.X_score) + '\n'
        score_text += 'Player 2 (O): ' + str(self.O_score) + '\n'
        score_text += 'Tie               : ' + str(self.tie_score)
        self.canvas.create_text(size_of_board / 3, 3 * size_of_board / 4, font="cmr 30 bold", fill= Green_color,
                                text=score_text)
        self.reset_board = True

        score_text = 'Click to play again \n'
        self.canvas.create_text(size_of_board / 2, 15 * size_of_board / 16, font="cmr 20 bold", fill="gray",
                                text=score_text)

    def convert_logical_to_grid_position(self, logical_position):
        logical_position = np.array(logical_position, dtype=int)
        return (size_of_board / 3) * logical_position + size_of_board / 6

    def convert_grid_to_logical_position(self, grid_position):
        grid_position = np.array(grid_position)
        return np.array(grid_position // (size_of_board / 3), dtype=int)

    def is_grid_occupied(self, logical_position):
        if self.board_status[logical_position[0]][logical_position[1]] == 0:
            return False
        else:
            return True

    def is_winner(self, player):

        player = -1 if player == 'X' else 1

        for i in range(3):
            if self.board_status[i][0] == self.board_status[i][1] == self.board_status[i][2] == player:
                return True
            if self.board_status[0][i] == self.board_status[1][i] == self.board_status[2][i] == player:
                return True

        if self.board_status[0][0] == self.board_status[1][1] == self.board_status[2][2] == player:
            return True

        if self.board_status[0][2] == self.board_status[1][1] == self.board_status[2][0] == player:
            return True

        return False

    def is_tie(self):

        r, c = np.where(self.board_status == 0)
        tie = False
        if len(r) == 0:
            tie = True

        return tie

    def is_gameover(self):
        self.X_wins = self.is_winner('X')
        if not self.X_wins:
            self.O_wins = self.is_winner('O')

        if not self.O_wins:
            self.tie = self.is_tie()

        gameover = self.X_wins or self.O_wins or self.tie

        if self.X_wins:
            print('X wins')
        if self.O_wins:
            print('O wins')
        if self.tie:
            print('Its a tie')

        return gameover

    def click(self, event):
        grid_position = [event.x, event.y]
        logical_position = self.convert_grid_to_logical_position(grid_position)

        if not self.reset_board:
            if self.player_X_turns:
                if not self.is_grid_occupied(logical_position):
                    self.draw_X(logical_position)
                    self.board_status[logical_position[0]][logical_position[1]] = -1
                    self.player_X_turns = not self.player_X_turns
            else:
                if not self.is_grid_occupied(logical_position):
                    self.draw_O(logical_position)
                    self.board_status[logical_position[0]][logical_position[1]] = 1
                    self.player_X_turns = not self.player_X_turns

            if self.is_gameover():
                self.display_gameover()

        else:  
            self.canvas.delete("all")
            self.play_again()
            self.reset_board = False


game_instance = Tic_Tac_Toe()
game_instance.mainloop()
