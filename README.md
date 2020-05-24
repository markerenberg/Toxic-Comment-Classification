# Toxic Comment Classification Kaggle
This repository contains code for my submission to the Toxic Comment Classification Challenge on Kaggle.
https://www.kaggle.com/c/jigsaw-toxic-comment-classification-challenge/overview

# Background of Competition
In this competition, competitors are challenged to build a multi-label text classifier that’s capable of detecting different types of toxicity. Toxicity is defined according to six categories: toxic, severe_toxic, obscene, threat, insult, identity_hate. The training and test data are derived from a dataset of comments from Wikipedia’s talk page edits.

# Solution

## Data Pre-processing
To clean each document in the corpus, the following steps are taken:
  1) Convert to lowercase
  2) Replace contractions (won't, didn't, it's, etc.)
  3) Remove non-alphabetic characters
  4) Remove extra whitespaces
  5) Tokenize document using WordPunctTokenizer from Natual Language Toolkit (NLTK) library.
  6) Filter out stop words using NLTK English stopwords corpus.

I also experimented with lemmatization and spell-check using this kernel: https://www.kaggle.com/cpmpml/spell-checker-using-word2vec/comments
However, I found that both of these extra steps degraded the scores of my final model when evaluated on the test set. 

## Feature Engineering
Feature engineering for this competition began with simple Bag-of-Words and TF-IDF scores. TF-IDF scores proved to be more effective, so I focused on that instead. Two types of vectorizers were fit, one on individual words, and then another on n-grams. The (2,6) n-gram range proved to be more stable than other combinations, and thus was my final choice. Stop words are also removed.

In addition to TF-IDF scores, extra metadata features were also added. These features include 

## Model Selection

## Model Performance
