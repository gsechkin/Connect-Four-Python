# AI Player for use in Connect Four   

import random  
from connect_four_folder import *

class AIPlayer(Player):
    """A subclass of Player that is an intelligent computer player that is
       designed to make the best possible moves based on a look ahead
    """
    def __init__(self, checker, tiebreak, lookahead):
        """constructor for new AIPlayer object which takes in 3 attributes
        """
        assert(checker == 'X' or checker == 'O')
        assert(tiebreak == 'LEFT' or tiebreak == 'RIGHT' or tiebreak == 'RANDOM')
        assert(lookahead >= 0)
        super().__init__(checker)
        self.tiebreak = tiebreak
        self.lookahead = lookahead
        
    def __repr__(self):
        """overrides the Player method and returns a string representation
           of the AIPlayer object including its new attributes
        """
        s = super().__repr__() 
        s += ' (' + self.tiebreak + ', ' + str(self.lookahead) + ')'
        return s
    
    def max_score_column(self, scores):
        """takes a list of scores and returns the index of the max score, using
           the indicated tiebreaking strategy if necessary
        """
        max_val = max(scores)
        new_lst = []
        for i in range(len(scores)):
            if scores[i] == max_val:
                new_lst += [i]
        if self.tiebreak == 'LEFT':
            return min(new_lst)
        elif self.tiebreak == 'RIGHT':
            return max(new_lst)
        elif self.tiebreak == 'RANDOM':
            return random.choice(new_lst)
            
    def scores_for(self, b):
        """takes a Board object b and determines the called AIPlayer‘s scores 
           for the columns in b
        """
        scores = [50] * b.width
        for col in range(b.width):
            if b.can_add_to(col) == False:
                scores[col] = -1
            elif b.is_win_for(self.checker) == True:
                scores[col] = 100
            elif b.is_win_for(self.opponent_checker()) == True:
                scores = [0] * b.width
            elif self.lookahead == 0:
                scores[col] = 50
            else:
                b.add_checker(self.checker, col)
                opp = AIPlayer(self.opponent_checker(), self.tiebreak, \
                              self.lookahead - 1)
                opp_score = opp.scores_for(b)
                if max(opp_score) == 0:
                    scores[col] = 100
                if max(opp_score) == 50:
                    scores[col] = 50
                if max(opp_score) == 100:
                    scores[col] = 0
                b.remove_checker(col)

        return scores
    
    def next_move(self, b):
        """overrides the next move function, and instead uses the AI's best
           judgement to make the next move based on scores and the tiebreak 
        """
        self.num_moves += 1
        AI_scores = self.scores_for(b)
        return self.max_score_column(AI_scores)
