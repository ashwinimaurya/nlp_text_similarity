# Generalized Edit Based Similairty (Distance) Functions for Comparing Strings


### What is Edit Distance between two strings?

Edit distance functions are used in many applications. For instance words completion, search engine (such as google) auto correction, mis-spelling detection etc are something we use almost every day.

Edit distance between two string is typically defined as number of insertion, deletion, substitutions, transpose etc of characters. There are different variants of the algorithms such as hamming distance (number of character positions two strings differe from each other), Levenshtein dstance (accounts for minimum number of insertion, deletion, and substitutions), Damerau - Levenshtien (accounts for minimum number of insertion, deletion, substitutions, and transpose), Jaro-Winkler (not a metric, an improvement of Jaro distance/similarity as it gives more weight to strings that have larger common prefixes, its based on matching count, a matching is defined if a character that appears in both string is at most max(string_1, string_2)/2) distance away). Among these distance functions, Jaro Winkler (as this gives some weightage to strings having common longer prefixes)  works works better than other but again this is use case specific. . 

Below I dicusss a variations of these edit distance functions which I would call as generalzied distance (similarity) fuctions. Analysis on some most popular homonyms (similar spelled but different in meaning) shows the generalzied distance metrics are generally better than original counterparts. For mispelled or similar words, the existing distance functions can be preferred than their generalzied counterparts,

Generalzied Edit Distance Functions:

      Intuition: 
           Typically different parts of speech of same words differ at towards at end of the strin beginning. Also mispelled words often are mispelled at middle or end of string. Therefore given two strings, more they match from the begniing, more liley they are similar words than if they match from end. The generalized distance/similarity functions conputes the distance between each substring from left, and then mean of all these distances. One can also use different weights for substrings, but again if that would be useful for a particular uses cases. 

      s1="dummy"
      s2="dummies"

      s1='dummy'
      s2='dummies'
      
      print(rapidfuzz.distance.Hamming.normalized_similarity(s1,s2))   
      print(rapidfuzz.distance.Levenshtein.normalized_similarity(s1,s2))
      print(rapidfuzz.distance.DamerauLevenshtein.normalized_similarity(s1,s2))
      print(get_generalized_fuzz_dl_norm_simi(s1, s2))

      0.5714285714285714
      0.5714285714285714
      0.5714285714285714
      0.8625850340136054

      for similar meaning strings, generalzied similarity works quite well in this example.

      Another example:
      
      s1='faithful'
      s2='fruitful'
      
      print(rapidfuzz.distance.Hamming.normalized_similarity(s1,s2))
      print(rapidfuzz.distance.Levenshtein.normalized_similarity(s1,s2))
      print(rapidfuzz.distance.DamerauLevenshtein.normalized_similarity(s1,s2))
      print(get_generalized_fuzz_dl_norm_simi(s1, s2))
      
      0.5
      0.625
      0.625
      0.5224702380952382

      for similar spelled words with different meaning, generalzied similarity works quite well in this example.
