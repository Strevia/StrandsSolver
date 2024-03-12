# Strands Solver
Recently, the New York Times released the beta of a new word-puzzle game, [Strands](https://www.nytimes.com/games/strands). As a self-proclaimed [Wordle aficionado](https://github.com/Strevia/WordleStuff) and serial bored person, I will be taking a crack at analyzing this game and attempting to solve it in the generalized case.
## Know the Rules
The Strands board contains a 6x8 grid of letters, as well as a specific number of words. Words are formed through connecting adjacent letters, similiar to a wordsearch. Unlike a wordsearch, in Strands, words do not need to form a straight line. Each letter will be used exactly once, and there is one "spangram" which stretches from one end of the board to the opposite end.

For example, the March 12 puzzle starts like this:

![](/screenshots/Screenshot%20from%202024-03-12%2016-51-23.png)

Solved, it looks like this:

![](/screenshots/Screenshot%20from%202024-03-12%2016-54-47.png)

The 8 words are "league", "fathom", "foot", "yard", "inch", "furlong", "meter", and "measurements". Measurements is the "spangram", stretching from end to end of the board.

## Preliminary Thoughts


After understanding the rules of the game, I have some preliminary thoughts:

- The game is definetly NP; it's trivial to check whether a given solution solves a board.
- No information is required from the game after the board is input. So, this game will be much easier than Wordle to solve (which requires output from the game after each guess).
- It's very possible for there to be multiple solutions to a given puzzle, since the wordlist could, hypothetically, contain any and every combination of letters. For this reason, I will be solving the problem of finding not just one solution, but all solutions to a given board.

I also want to specify what I mean by "generalized case". In the NYT version of the game, there are very specific words which are allowed. In addition, there is a caveat that words must be at least three letters long. However, when creating the solution, the wordlist should be able to be any specified list of words. I'd ideally like for it not to matter what exact wordlist is used for the solution. For my solution, I will use the dictionary at /usr/share/dict/words, for simplicity.

## The Algorithm

To solve Strands I believe the best and simplest way is to divide the problem into two steps:

1. Find all possible words which can be made from the letters on the board (this will be more than just the solution words).
1. With the possible words, find which combinations of them contain every letter on the board exactly once and contain a spangram.

Steps 1 and 2 can be solved indepedently, as long as the output from step 1 is valid for step 2. 

For Step 1, I am going to start with a simple brute force approach, checking every path of adjacent letters until the path is no longer a valid word. For example, starting from the Y in yard, "yo" is a valid beginning to multiple words, however "yoo" is not.

For Step 2, I plan to start by finding all spangrams, and then checking increasing sizes of combinations until one of the right size is found.

All in all, I think this will be a relatively simple proof of concept. If it is, I will try to optimize the algorithm for speed.