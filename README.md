# Pun Finder API

## Sources
Uses truncated version of [The Carnegie Mellon University Pronouncing Dictionary](http://www.speech.cs.cmu.edu/cgi-bin/cmudict)

## Method
//ToDo: expand

- Determines the pronounciation array ([AE1, P, AH0, L] for APPLE)
  - Guesses a pronounciation arry if a word is not found
    - This is done by segmenting all words into consonant/vowel groups
    - Consonant sounds are merged and then mapped andmost frequent sound for group of letters is picked
    - not perfect though...
    - e.g. a|ft|e|rw|a|rd maps to [AE1, FT, ER0W, ER0D] -> a/AE1, ft/FT, rw/ER0W, a/ER0D, rd/?
- Matches current word with all other words giving
  - 1 point per sound perfectly matched
  - 0.65 points for sound almost matches [AE0, AE1]
  - 0.35 points for sound barely mathing [AE0, AH0]
  - 0 points for no match
- Matches occur two ways since "pun" should return "pencil" AND vice versa
- Similarity is given as value points recieved by tested word / points received by queried word
- Ranks based on frequency of word usage and similarity percentage

## Usage
API endpoint
https://pungenerator.herokuapp.com/?q=<query>&amount=<amount>&compre=<comprehensive search?>
- 'q' | string : query
- 'amount' | integer : amount of results to return
- 'compre' | boolean : whether to search for more words or not