# Artificial Intelligence Nanodegree
## Introductory Project: Diagonal Sudoku Solver

# Question 1 (Naked Twins)
Q: How do we use constraint propagation to solve the naked twins problem?  
A: *See answer below*

Naked twin strategy is not meant to solve a sudoku problem. However, it is of many strategies used to narrow down possible values in every box on the grid.

**Implementation & explanation:**

1. In our program, naked twin strategy is implemented within naked_twin method.
    > def naked_twin(values)
    
    This naked_twin method takes in parameter "values". This parameter comes from reduce_puzzle method after the given sudoku problem went through elimination and only_choice methods.
    
2. Our algorithm will loop through each unitlist and box and find naked twin pairs.
    ~~~~
    for unit in unitlist:
        unit_values = [values[box] for box in unit]
        twins = [v for v in unit_values if unit_values.count(v) == 2 and len(v) == 2]
    ~~~~
    
    To find a naked_twin pair, loop through every box and find a value with a pair number that appears twice in unitlist. Save naked_twin pairs in twins arrary.

3. Once our algorithm identifies all naked_twins value, loop through the boxes again and eliminate any values that contain every digit in naked_twin pairs.
    ~~~~
    for twin in twins:
            for i in twin:
                for box in unit:
                    if values[box] != twin:
                        values = assign_value(values, box, values[box].replace(i, ''))
    ~~~~
    The last 2 lines above will reduce the possible values in any box that contains any digits from naked twin pairs. 
    
    Assign_value will visualize sudoku solver on pygame.


**Our naked_twin algorithm:**
~~~~
def naked_twins(values):

    for unit in unitlist:
        unit_values = [values[box] for box in unit]
        twins = [v for v in unit_values if unit_values.count(v) == 2 and len(v) == 2]
        for twin in twins:
            for i in twin:
                for box in unit:
                    if values[box] != twin:
                        values = assign_value(values, box, values[box].replace(i, ''))

    return values
~~~~

# Question 2 (Diagonal Sudoku)
Q: How do we use constraint propagation to solve the diagonal sudoku problem?  
A: *See answer below*

Peter Norvig's "classic sudoku" solver consists of 9x9 grid and 3 units, ie. row, column, and 3x3 box. Together these 3 units become a unitlist and the squares that share a unit are called peers.
 
For "diagonal sudoku" solver, we will expand the unitlist with 2 diagonal lines. The rules and solver should comply with classic sudoku as well.

Diagonal sudoku rules: [click link here](http://rohanrao.blogspot.com/2008/09/rules-of-diagonal-sudoku_29.html)

**Implementation:**

1. Create 2 new units for 2 diagonal lines
    ~~~~
    diagonal1 = [[rows[i]+cols[i] for i in range(len(rows))]]
    diagonal2 = [[rows[i]+cols[::-1][i] for i in range(len(rows))]]
    ~~~~
    
2. Add the above diagonal units into the classic unitlist
    > unitlist = row_units + col_units + square_units + diagonal1 + diagonal2




### Install

This project requires **Python 3**.

We recommend students install [Anaconda](https://www.continuum.io/downloads), a pre-packaged Python distribution that contains all of the necessary libraries and software for this project. 
Please try using the environment we provided in the Anaconda lesson of the Nanodegree.

##### Optional: Pygame

Optionally, you can also install pygame if you want to see your visualization. If you've followed our instructions for setting up our conda environment, you should be all set.

If not, please see how to download pygame [here](http://www.pygame.org/download.shtml).

### Code

* `solutions.py` - You'll fill this in as part of your solution.
* `solution_test.py` - Do not modify this. You can test your solution by running `python solution_test.py`.
* `PySudoku.py` - Do not modify this. This is code for visualizing your solution.
* `visualize.py` - Do not modify this. This is code for visualizing your solution.

### Visualizing

To visualize your solution, please only assign values to the values_dict using the ```assign_values``` function provided in solution.py

### Data

The data consists of a text file of diagonal sudokus for you to solve.