class Board:
    """A class that stores and manipulates a board of any dimensions, desgined
       for connect 4
    """
    def __init__(self, height, width):
        """constructor that initializes the height and width of board
        """
        self.height = height
        self.width = width
        self.slots = [[' '] * self.width for row in range(self.height)]
        
    def __repr__(self):
        """ Returns a string representation for a Board object.
        """
        s = ''         
        for row in range(self.height):
            s += '|'   

            for col in range(self.width):
                s += self.slots[row][col] + '|'
            s += '\n' 
        s += '-' * (self.width * 2) + '-'
        s += '\n'
        for col in range(self.width):
            num = str(col % 10)
            s += ' ' + num 

        return s
    
    def add_checker(self, checker, col):
        """takes two inputs; a checker being either an 'X' or an 'O' and a 
           col that is the index of the column in which the checker is to be
           added, and adds that checker to the board
        """
        assert(checker == 'X' or checker == 'O')
        assert(0 <= col < self.width)
        if self.slots[self.height - 1][col] == ' ':
            self.slots[self.height - 1][col] = checker
        else:
            row = 0
            while self.slots[row +1][col] == ' ':
                row += 1
            self.slots[row][col] = checker
    
    def reset(self):
        """resets the Board object on which it is called by setting all slots 
           to contain a space character
        """
        self.slots = [[' '] * self.width for row in range(self.height)]
        
    def add_checkers(self, colnums):
        """ takes in a string of column numbers and places alternating
            checkers in those columns of the called Board object, 
            starting with 'X'.
        """
        checker = 'X'

        for col_str in colnums:
            col = int(col_str)
            if 0 <= col < self.width:
                self.add_checker(checker, col)

            if checker == 'X':
                checker = 'O'
            else:
                checker = 'X'
            
    def can_add_to(self, col):
        """returns True if it is valid to place a checker in the column col on 
           the calling Board object, and otherwise returns False
        """
        if -1 < col < self.width:
            if self.slots[0][col] == ' ':
                return True
        return False
    
    def is_full(self):
        """return True if the board is full of checkers and False otherwise
        """
        for col in range(self.width):
            if self.can_add_to(col) == True:
                return False
        return True
    
    def remove_checker(self, col):
        """removes the top checker from column col of the called Board object.
           If the column is empty, then the method should do nothing
        """
        if self.slots[self.height - 1][col] != ' ':
            row = 0
            while self.slots[row][col] == ' ':
                row += 1
            self.slots[row][col] = ' '
    
    def is_horizontal_win(self, checker):
        """ Checks for a horizontal win for the specified checker.
        """
        for row in range(self.height):
            for col in range(self.width - 3):
               if self.slots[row][col] == checker and \
                  self.slots[row][col + 1] == checker and \
                  self.slots[row][col + 2] == checker and \
                  self.slots[row][col + 3] == checker:
                   return True
        return False
    
    def is_vertical_win(self, checker):
        """ Checks for a vertical win for the specified checker.
        """
        for row in range(self.height - 3):
            for col in range(self.width):
                if self.slots[row][col] == checker and \
                   self.slots[row + 1][col] == checker and \
                   self.slots[row + 2][col] == checker and \
                   self.slots[row + 3][col] == checker:
                    return True
        return False
    
    def is_diagonal_LR_win(self, checker):
        """ Checks for a left to right diagonal win for the checker
        """
        for row in range(self.height - 3):
            for col in range(self.width -3):
                if self.slots[row][col] == checker and \
                   self.slots[row + 1][col + 1] == checker and \
                   self.slots[row + 2][col + 2] == checker and \
                   self.slots[row + 3][col + 3] == checker:
                    return True
        return False
    
    def is_diagonal_RL_win(self, checker):
        """ Checks for a right to left diagonal win for the checker
        """
        for row in range(self.height - 3):
            for col in range(3, self.width):
                if self.slots[row][col] == checker and \
                   self.slots[row + 1][col - 1] == checker and \
                   self.slots[row + 2][col - 2] == checker and \
                   self.slots[row + 3][col - 3] == checker:
                    return True
        return False    
    
    def is_win_for(self, checker):
        """accepts a parameter checker that is either 'X' or 'O', and returns 
           True if there are four consecutive slots containing checker on the 
           board. Otherwise, it should return False
        """
        assert(checker == 'X' or checker == 'O')
        if self.is_horizontal_win(checker) == True or \
           self.is_vertical_win(checker) == True or \
           self.is_diagonal_LR_win(checker) == True or \
           self.is_diagonal_RL_win(checker) == True:
               return True
        return False
