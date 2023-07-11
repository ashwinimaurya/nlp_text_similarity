# Generalized Edit Based Similairty (Distance) Functions for Comparing Strings


### What is Edit Distance between two strings?

Edit distance between two string is typically defined as number of addition, deletion, insertion, transpose etc of characters. Some of the popular 
edit distace functions are hamming distance, Levenshitein distance, Levenshtein Ratio, damerauLevenshtein, Jaro Winkler distance etc. 
Below I propose variations of these edit distance functions which are called generalzied distance fuctions. Analysis on some of most mispelled words, and homonyms (similar spelled but different in meaning)
shows the generalzied distance metrics are generally better than original counterparts.


 Generalzied Edit Distance Functions:
       Hamming Distance: 
      The hamming distance betwee two strings is defined as number of positions where two strings differ. For example for below strings:

      s1="Mac and Cheese"
      s2="Mak and Cheeze"

      the hamming distance would be 2.  c <> k ad s<>z. For below two strings:
      
      If one of string is empty, the hamming distance is length of non empty string.
  
### 2. Levenshtein Distance: 
      
      The Levenshtein distance between two strings is defined is minumum number of (insertions, deletion, substitution) needed to convert one string to other. Here is Wiki page: https://en.wikipedia.org/wiki/Levenshtein_distance      

      s1="Adam"
      s2="Adm"

      the Levenshtein distance would be 1.  Just insert 'a' in string s2 at position 2 makes both strings same.

      If one of string is empty, the Levenshtein distance is length of non empty string.

      #### How to get in Python packages:
        
        Its available in many packages. One can use Levenshtein, rapidfuzz. 

        Code:

        import rapidfuzz
        
        print(rapidfuzz.distance.Levenshtein.distance(s1,s2))
        
                
      

      

      
