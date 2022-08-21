# Quora-Question-Answering

Problem Statement
https://www.kaggle.com/competitions/quora-question-pairs/overview

Currently, Quora uses a Random Forest model to identify duplicate questions. 
In this competition, Kagglers are challenged to tackle this natural language processing problem by applying advanced techniques to classify whether 
question pairs are duplicates or not. 
Doing so will make it easier to find high quality answers to questions resulting in an improved experience for Quora writers, seekers, and readers.

Dataset Link : https://www.kaggle.com/competitions/quora-question-pairs/data

#### Example Data point 
"id","qid1","qid2","question1","question2","is_duplicate"
"0","1","2","What is the step by step guide to invest in share market in india?","What is the step by step guide to invest in share market?","0"
"1","3","4","What is the story of Kohinoor (Koh-i-Noor) Diamond?","What would happen if the Indian government stole the Kohinoor (Koh-i-Noor) diamond back?","0"
"7","15","16","How can I be a good geologist?","What should I do to be a great geologist?","1"
"11","23","24","How do I read and find my YouTube comments?","How can I see all my Youtube comments?","1"

### Feature Extraction:
- ##### Basic Features - Extracted some features before cleaning of data as below.
  - <b>freq_qid1</b> = Frequency of qid1's
  - <b>freq_qid2</b> = Frequency of qid2's
  - <b>q1len</b> = Length of q1
  - <b>q2len</b> = Length of q2
  - <b>q1_n_words</b> = Number of words in Question 1
  - <b>q2_n_words</b> = Number of words in Question 2
  - <b>word_Common</b> = (Number of common unique words in Question 1 and Question 2)
  - <b>word_Total</b> =(Total num of words in Question 1 + Total num of words in Question 2)
  - <b>word_share</b> = (word_common)/(word_Total)
  - <b>freq_q1+freq_q2</b> = sum total of frequency of qid1 and qid2
  - <b>freq_q1-freq_q2</b> = absolute difference of frequency of qid1 and qid2
- #### Advanced Features
    1. Token Features
    - cwc_min: This is the ratio of the number of common words to the length of the smaller question
    - cwc_max: This is the ratio of the number of common words to the length of the larger question
    - csc_min: This is the ratio of the number of common stop words to the smaller stop word count among the two questions
    - csc_max: This is the ratio of the number of common stop words to the larger stop word count among the two questions
    - ctc_min: This is the ratio of the number of common tokens to the smaller token count among the two questions
    - ctc_max: This is the ratio of the number of common tokens to the larger token count among the two questions
    - last_word_eq: 1 if the last word in the two questions is same, 0 otherwise
    - first_word_eq: 1 if the first word in the two questions is same, 0 otherwise
    2. Length Based Features
    - mean_len: Mean of the length of the two questions (number of words)
    - abs_len_diff: Absolute difference between the length of the two questions (number of words)
    - longest_substr_ratio: Ratio of the length of the longest substring among the two questions to the length of the smaller question
    3. Fuzzy Features
    - fuzz_ratio: fuzz_ratio score from fuzzywuzzy
    - fuzz_partial_ratio: fuzz_partial_ratio from fuzzywuzzy
    - token_sort_ratio: token_sort_ratio from fuzzywuzzy
    - token_set_ratio: token_set_ratio from fuzzywuzzy

### Model Used:
Random Forest,XGBoost

### Results
| Model | Features Used | Accuracy |
------- | ------------- | -------- |
| Random Forest  | No extra feature  | 73.85  |
| XGBoost        | No extra feature  | 68.72  |
| Random Forest  | Basic Feature  | 77.48  |
| XGBoost        | Basic Feature  | 73.13  |
| Random Forest  | Basic + Advance Feature  | 78.55  |
| XGBoost        | Basic + Advance Feature  | 75.96  |
