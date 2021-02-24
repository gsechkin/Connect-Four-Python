# Playing the game 

from connect_four_folder import Board
from connect_four_folder import Player
import random

class RandomPlayer(Player):
    """subclass of Player class that represents an unintelligent computer 
       player that chooses at random from the available columns
    """
    def next_move(self, b):
        """overrides the method, and instead chooses at random from the columns
           in the board b that are not yet full, and return the index of that
           randomly selected column. Also increments the number of moves
        """
        self.num_moves += 1
        lst = []
        for col in range(b.width):
            if b.can_add_to(col) == True:
                lst += [col]
        return random.choice(lst)
    
def process_move(p, b):
    """takes as parameters a Player object and a Board object, and processes
       the next move by printing which turn it is, obtaining the next move,
       applying the move to the board, print the board, check to see if the
       player wins or ties and prints the appropriate message
    """
    s = str(p) + "'s turn"
    print(s)
    col = p.next_move(b)
    b.add_checker(p.checker, col)
    print()
    print(b)
    if b.is_win_for(p.checker) == True:
        s = str(p) + ' wins in ' + str(p.num_moves) + \
        ' moves.\nCongratulations!'
        print(s)
        return True
    if b.is_full() == True:
        print('Its a tie!')
        return True
    return False
        
    
def connect_four(p1, p2):
    """ Plays a game of Connect Four between the two specified players,
        and returns the Board object as it looks at the end of the game.
        inputs: p1 and p2 are objects representing Connect Four
          players (objects of the Player class or a subclass of Player).
          One player should use 'X' checkers and the other should
          use 'O' checkers.
    """
    # Make sure one player is 'X' and one player is 'O'.
    if p1.checker not in 'XO' or p2.checker not in 'XO' \
       or p1.checker == p2.checker:
        print('need one X player and one O player.')
        return None

    print('Welcome to Connect Four!')
    print()
    b = Board(6, 7)
    print(b)
    
    while True:
        if process_move(p1, b) == True:
            return b

        if process_move(p2, b) == True:
            return b
