# TalmudAI-AIUCD2025
# Introduction
This page presents the interactions conducted with llama-3.1-70b-versatile for Hebrew-Aramaic to Italian translation support. Prompts and responses will be provided in Italian.

We randomly selected a total of N source-target pairs from the Talmud, each accompanied by translation memory (TM) suggestions. Each hint contained the source string, the target string (i.e., the translation), and the similarity score between the source and the suggested source.
We then filtered the pairs keeping only those with at least 3 suggestions with a similarity score greater than or equal to 50%. The resulting 66 pairs were provided to the LLM for translation, first without the suggestions and then with a context composed of the list of suggestions.

Rating measures were calculated for the candidate translations against the domain expert-verified target, and the delta between the version with and without suggestions was derived for each. The measures used are: SacreBLEU, BERTscore and Meteor score.
# Source and Target
Source indicates the original Hebrew-Aramaic string, while target indicates the Italian translation. The translation provided by a domain expert is considered the gold standard.
# Prompt template without context
    Inserire qui il prompt senza contesto
# Prompt template with context
    Inserire qui il prompt con contesto
# Results
Out of 66 pairs, for 54 we found higher scores for the translation provided by an LLM with context. 


|| **SacreBLEU** | **BERTscore** | **Meteor** |
| ------------- | ------------- | ------------- | ------------- |
| **LLM+TM** | 0,5869 | 0,7695 | 0,3551 |
| **LLM** | 0,1845 | 0,8911 | 0,7180 |
| **(LLM+TM)-LLM** | 218,07% | 15,80% | 102,17% |


The remaining 12 pairs have at least one measure with a negative delta.

We asked a domain expert to evaluate these 12 pairs by anonymizing the origin of the contained strings. The results of the evaluation indicate that out of 12 pairs were identified:

- 5 cases in which both translations were acceptable;
- 2 cases in which the translation of the LLM alone is acceptable;
- 2 cases in which the translation of the LLM with TM is acceptable;
- 3 cases in which no candidate translation was acceptable.
# Complete Output
