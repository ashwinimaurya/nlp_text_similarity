# Generalized Edit Based Similairty (Distance) Functions for Comparing Strings


### What is Edit Distance between two strings?

Edit distance between two string is typically defined as number of addition, deletion, insertion, transpose etc of characters. Some of the popular 
edit distace functions are hamming distance, Levenshitein distance, Levenshtein Ratio, damerauLevenshtein, Jaro Winkler distance etc. 
Below I propose variations of these edit distance functions which are called generalzied distance fuctions. Analysis on some of mst mispelled words, and homonyms (similar spelled but different in meaning)
shows the generalzied distance metrics are generally better than original counterparts.


### 1. Hamming Distance: 
      The hamming distance betwee two strings is defined as number of positions where two strings differ. For example for below strings:

      s1="Mac and Cheese"
      s2="Mak and Cheeze"

      the hamming distance would be 2.  c <> k ad s<>z. For below two strings:
      
      s1="Mac and C"
      s2="Pizza"

      we can compare these strings for each character position:  
      distance between (M,P)=1
      distance between (a,i)=1
      distance between (c,z)=1
      distance between (' ',z)=1
      distance between (a,a)=0
      distance between (n,'')=1
      distance between (d,'')=1
      distance between (' ','')=1
      distance between (C,'')=1

      therefore hamming distance=1+1+1+1+0+1+1+1+1=8

      If one of string is empty, the hamming distance is length of non empty string.

      #### How to get in Python packages:
        Its available in many packages. One can use Levenshtein, rapidfuzz. 

        Code:

        import rapidfuzz
        
        s1="Mac and Cheese"
        s2="Mak and Cheeze
        
        print(rapidfuzz.distance.Hamming.distance(s1,s2))
        
        
      

      

      
