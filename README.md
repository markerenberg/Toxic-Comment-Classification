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

I also experimented with lemmatization and spell-check using this kernel: https://www.kaggle.com/cpmpml/spell-checker-using-word2vec/comments.
However, I found that both of these extra steps degraded the scores of my final model when evaluated on the test set. 

## Feature Engineering
### TF-IDF Features
Feature engineering for this competition began with simple Bag-of-Words and TF-IDF scores. TF-IDF scores proved to be more effective, so I focused on that instead. Two types of vectorizers were fit, one on individual words, and then another on n-grams. The (2,6) n-gram range proved to be more stable than other combinations, and thus was my final choice. Stop words are also removed.

### Metadata Features
In addition to TF-IDF scores, extra metadata features were also added. These features include information about the count of words, characters, the ratio of uppercase letters and certain punctuation, and discrete counts of certain curse words. 

### POS + Spam Features
Features were also added to count the number of words according to their Part-of-Speech tag (ex. counting the number of adjectives). In addition, features were also created to determine if a comment was spam or not (based on ratio of repeating words).

### Word Embedding Features
I also experimented a lot with features derived from word embeddings. Initially, I trained FastText and Word2Vec models from scratch on the corpus, and used a TF-IDF weighted average of the word vectors for each document to compile a document vector. 

After finding that these results did not perform better than the base TF-IDF features, I also trained a Doc2Vec model from scratch on the corpus, and used both weighted and non-weighted averages of vectors to create a document vector. Unfortunately, these features also did not prove to be better than the base features, and lead to overfitting of the model.

## Dealing with Class Imbalance
In this competition, there was a severe class imbalance in the number of positive labels vs negative labels. 

## Model Selection



## Model Performance
