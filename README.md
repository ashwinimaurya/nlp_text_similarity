# Generalized Edit Distance (Similarrity)

## What is Edit Distance (similarity) between two strings?
Edit distance functions are used in many applications. For instance, in words completion, search engine (such as google) auto correction, mis-spelling detection etc are some uses cases we encounter almost every day.

Edit distance between two string is typically defined as number of insertion, deletion, substitutions, transpose etc of characters. There are different variants of the algorithms such as hamming distance (number of character positions two strings different from each other), Levenshtein distance (accounts for minimum number of insertion, deletion, and substitutions), Damerau-Levenshtien (accounts for minimum number of insertion, deletion, substitutions, and transpose), Jaro-Winkler (not a metric, is an improvement of Jaro distance/similarity as it gives more weight to strings that have larger common prefixes, based on matching count: a matching is defined if a character that appears in both string is at most max(string_1, string_2)/2) distance away). Among these distance functions, Jaro Winkler works better than others but again this depends upon application.

Below I discuss a variations of these edit distance functions which I would call as generalized distance (similarity) functions. Analysis on some most popular homonyms (similar spelled but different in meaning) shows the generalized distance metrics are generally better than original counterparts. For misspelled or similar words, the existing distance functions can be preferred than their generalized counterparts,

## Generalized Similarity (distance) Function
Intuition: Typically different parts of speech of same words differ at towards at end of the string beginning. Also misspelled words often are misspelled at middle or end of string. Therefore given two strings, more they match from the beginning, more likely they are similar words than if they match from end. The generalized distance/similarity functions computes the distance between each substring from left, and then mean of all these distances. One can also use different weights for substrings, but again if that would be useful for a particular uses cases.

## Here is Python implementation:

     def get_generalized_DamerauLevenshtein_similarity(s1,s2):
          """
          Compute the generalized similarity betwee two strings
          """
          
          from itertools import zip_longest
          import rapidfuzz
          if s1=='' or s2=='':
              return 0
          
          s1=s1.lower()
          s2=s2.lower()
          t1=''
          t2=''
          
          simi=0; cnt=0
          for a,b in zip_longest(s1,s2):
              if a:
                  t1=t1+a
              if b:
                  t2=t2+b
              cnt+=1
              simi+=rapidfuzz.distance.DamerauLevenshtein.normalized_similarity(t1,t2)
              
          return simi/cnt

### Example 1:

     import rapidfuzz, numpy as np
     
     s1='dummy'
     s2='dummies'
     
     print(f'Hamming similarity is :                           {np.round(rapidfuzz.distance.Hamming.normalized_similarity(s1,s2),3)}')
     print(f'Levenshtein similarity is :                       {np.round(rapidfuzz.distance.Levenshtein.normalized_similarity(s1,s2),3)}')
     print(f'Damerau-Levenshtein similairty is :               {np.round(rapidfuzz.distance.DamerauLevenshtein.normalized_similarity(s1,s2),3)}')
     print(f'Generalized Damerau-Levenshtein similairty is :   {np.round(get_generalized_fuzz_dl_norm_simi(s1, s2),3)}\n')
     
     print(f'Jaro Winkler Similairty is :                      {np.round(rapidfuzz.distance.JaroWinkler.normalized_similarity(s1,s2),3)}')
     print(f'Generalized Jaro Winkler Similairty is :          {np.round(get_generalized_jaro_winkler_similarity(s1,s2),3)}')
     
     Hamming similarity is :                           0.571
     Levenshtein similarity is :                       0.571
     Damerau-Levenshtein similairty is :               0.571
     Generalized Damerau-Levenshtein similairty is :   0.863
     
     Jaro Winkler Similairty is :                      0.874
     Generalized Jaro Winkler Similairty is :          0.955

for similar meaning strings, generalized similarity works quite well in this example. Generalized Jaro Winkler similarity seems to better than standard Jaro Winkler similarity (JW is skewed towards strings having larger common prefix).

### Example 2:

       s1='faithful'
       s2='fruitful'
       
       print(f'Hamming similarity is :                           {np.round(rapidfuzz.distance.Hamming.normalized_similarity(s1,s2),3)}')
       print(f'Levenshtein similarity is :                       {np.round(rapidfuzz.distance.Levenshtein.normalized_similarity(s1,s2),3)}')
       print(f'Damerau-Levenshtein similairty is :               {np.round(rapidfuzz.distance.DamerauLevenshtein.normalized_similarity(s1,s2),3)}')
       print(f'Generalized Damerau-Levenshtein similairty is :   {np.round(get_generalized_fuzz_dl_norm_simi(s1, s2),3)}\n')
     
       print(f'Jaro Winkler Similairty is :                      {np.round(rapidfuzz.distance.JaroWinkler.normalized_similarity(s1,s2),3)}')
       print(f'Generalized Jaro Winkler Similairty is :          {np.round(get_generalized_jaro_winkler_similarity(s1,s2),3)}')
       
       Hamming similarity is :                           0.5
       Levenshtein similarity is :                       0.625
       Damerau-Levenshtein similairty is :               0.625
       Generalized Damerau-Levenshtein similairty is :   0.522
       
       Jaro Winkler Similairty is :                      0.85
       Generalized Jaro Winkler Similairty is :          0.766

for similar spelled words with different meaning, generalized similarity works quite well in this example.
