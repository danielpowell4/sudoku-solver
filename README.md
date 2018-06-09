# Sudoku Solver

A simple python script that solves a sudoku string.

## Overview

This script uses 5 functions in an attempt to solve the puzzle, first input as
a string of length 81

For example:

**Starting:**

`..3.2.6..9..3.5..1..18.64....81.29..7.......8..67.82....26.95..8..2.3..9..5.1.3..`

**Result:**

`483921657967345821251876493548132976729564138136798245372689514814253769695417382`

### 1. grid_values

Take a string and return a dictionary with a key of the square's label with the
value of either the solution or all digits (1-9)

This is done by using python's built in zip function to iterate through:

* an array that represents the solved or possible options for the input string, and
* the boxes which are built from a cross of rows and columns

### 2. eliminate

As the name suggests, this function eliminates choices from a square if one of
its peer boxes (from the column, row or square) already have that value selected.
In other words, this is the set that reduces the unknowns from 1-9 to only the
options remaining among its peers.

### 3. only_choice

After eliminate, each value is keyed with a reduced set of possible options.
Within a unit (column, row, square) many options will be the same. Some of the
options will only belong to one square. When this is the case, this only_choice
is selected.

### 4. reduce_puzzle

For many simple puzzles, looping through 'eliminate' and 'only_choice' will
yield the solution. This function runs these functions over and over. When
a solution is met or these two methods stop finding answers, the while loop ends
and returns what is known.

### 5. search

When reduce puzzle can't find an answer, gotta start somewhere and brute force
see if anything comes of it. Here, we tackle this by starting when the fewest
possible options exist and then filling in elsewhere.

In CS terms, this is called depth-first recursion. False-y values are captured
in reduce_puzzle and escaped at the top of search

## How can I see it?

The function `display` in utils.py can be used to print the value dictionaries
in a more human readable format a la:

```
. . 3 |. 2 . |6 . .
9 . . |3 . 5 |. . 1
. . 1 |8 . 6 |4 . .
------+------+------
. . 8 |1 . 2 |9 . .
7 . . |. . . |. . 8
. . 6 |7 . 8 |2 . .
------+------+------
. . 2 |6 . 9 |5 . .
8 . . |2 . 3 |. . 9
. . 5 |. 1 . |3 . .
```

---

This was written while working through Udacity's AI/Machine Learning programs
June 9, 2018
