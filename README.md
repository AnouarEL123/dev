# dev



#hhhhhhhhhhhh


from tkinter import *
import random

class XO(Tk):
    players = ["X", "O"]
    player = random.choice(players)

    def __init__(self):
        super().__init__()
        self.title("XO Game")
        self.geometry("400x520")

        self.lb = Label(self, text=(XO.player + " turn!"), font=("Arial", 30))
        self.lb.pack(side="top")
        self.btn = Button(self, text="Restart", font=("Arial", 30), command=self.restart)
        self.btn.pack(side="top")
        self.f = Frame(self)
        self.f.pack()

        self.buttons = [[None, None, None], [None, None, None], [None, None, None]]  # Buttons
        self.board_state = [[0, 0, 0], [0, 0, 0], [0, 0, 0]]  # Game state

        for i in range(3):
            for j in range(3):
                self.buttons[i][j] = Button(self.f, text="", font=("Arial", 30), width=5, height=2,command=lambda i=i, j=j: self.click(i, j))
                self.buttons[i][j].grid(row=i, column=j)

    def click(self, i, j):
        if XO.player == "X":
            if self.buttons[i][j]["text"] == "":
                self.lb.config(text="O turn!")
                self.buttons[i][j].config(text="X", state="disabled")
                self.board_state[i][j] = "X"  # Update game state
                XO.player = "O"
        elif XO.player == "O":
            if self.buttons[i][j]["text"] == "":
                self.lb.config(text="X turn!")
                self.buttons[i][j].config(text="O", state="disabled")
                self.board_state[i][j] = "O"  # Update game state
                XO.player = "X"

    def restart(self):
        for i in range(3):
            for j in range(3):
                self.buttons[i][j].config(text="", state="normal")  # Reset button text and state
                self.board_state[i][j] = 0  # Reset game state
        XO.player = random.choice(XO.players)  # Randomly choose the next player
        self.lb.config(text=(XO.player + " turn!"))  # Update the label text


a = XO()
a.mainloop()



