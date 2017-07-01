# AIND---Solve-Sudoku-with-AI
A Sudoku Solving AI that uses strategies like Eliminate, Only Choice, Search and Naked Twins.
# Artificial Intelligence Nanodegree
## Introductory Project: Diagonal Sudoku Solver

# Question 1 (Naked Twins)
Q: How do we use constraint propagation to solve the naked twins problem?  
A: Firstly we list out all the boxes with value length of 2 digits. Then we identify of naked twin for every box from its peers by checking if their values are equal or not. Once we have our naked twins we remove the value of naked twins from peers of both twins.
```
def naked_twins(values):
    """Eliminate values using the naked twins strategy.
    Args:
        values(dict): a dictionary of the form {'box_name': '123456789', ...}

    Returns:
        the values dictionary with the naked twins eliminated from peers.
    """

    # Find all instances of naked twins
    # List of boxes with 2 digit values in values dict
    two_digit_values = [box for box in values.keys() if len(values[box]) == 2]

    # # List of all eligible naked twins from two_digit_vales
    naked_twins = [[box1, box2] for box1 in two_digit_values for box2 in peers[box1] if set(values[box1])==set(values[box2])]
    
    # # Eliminate the naked twins as possibilities for their peers
    for twin in naked_twins:
        twin_box1 = twin[0]
        twin_box2 = twin[1]
    # Comman peers of the twin pair
        comman_peers = set(peers[twin_box1]) & set(peers[twin_box2])
        refined_peers = {box for box in comman_peers if len(values[box])>2}
        for peer in refined_peers:
            for value in values[twin_box1]:
                values = assign_value(values, peer, values[peer].replace(value, ''))
    return values

``` 

# Question 2 (Diagonal Sudoku)
Q: How do we use constraint propagation to solve the diagonal sudoku problem?  
A: To solve diagonal sudoku problem, we simply add the diagonal units to unitlist. This adds the diagonals to the peers of particular boxes.
```
diag1 = [[rows[i]+cols[i] for i in range(len(rows))]]
diag2 = [[rows[i]+cols_rev[i] for i in range(len(rows))]]
diag_units = diag1 + diag2
diagonal = True #Change to False for non-diagonal sudoku
if diagonal:
    unitlist = row_units + column_units + square_units + diag_units
else:
    unitlist = row_units + column_units + square_units
    
units = dict((s, [u for u in unitlist if s in u]) for s in boxes)
peers = dict((s, set(sum(units[s],[]))-set([s])) for s in boxes)

```

### Install

This project requires **Python 3**.

We recommend students install [Anaconda](https://www.continuum.io/downloads), a pre-packaged Python distribution that contains all of the necessary libraries and software for this project. 
Please try using the environment we provided in the Anaconda lesson of the Nanodegree.

##### Optional: Pygame

Optionally, you can also install pygame if you want to see your visualization. If you've followed our instructions for setting up our conda environment, you should be all set.

If not, please see how to download pygame [here](http://www.pygame.org/download.shtml).

### Run

* `solution.py` - You'll fill this in as part of your solution.
* `solution_test.py` - Do not modify this. You can test your solution by running `python solution_test.py`.
* `PySudoku.py` - Do not modify this. This is code for visualizing your solution.
* `visualize.py` - Do not modify this. This is code for visualizing your solution.
