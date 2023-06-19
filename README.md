# Sentence Reordering

Project for the course of Deep Learning at the University of Bologna, Master's Degree in Artificial Intelligence.

## Description
The aim of this project is to implement a model that is able to reorder sentences given in input. 

For instance, given the sequence of words
> to henry at be first france the king wanted with of friends

the model should be able to reorder the words in the correct order
> at first henry wanted to be friends with the king of france

The sentences are taken from the [Wikipedia 20220301 Simple dataset](https://huggingface.co/datasets/wikipedia/viewer/20220301.simple/train).

We only took sentences with a minimum length of 4 words and a maximum length of 32 words.

Constraints of the project:
- The model must be implemented in Tensorflow+Keras
- The model should have at most 20M parameters
- No pre-trained models should be used
## Model

The model is based on the [Transformer tutorial by Tensorflow](https://www.tensorflow.org/text/tutorials/transformer) with the following modifications:
- Single embedder for both encoder and decoder
- No positional encoding in the encoder, since the order of the words is not important

## Techniques used

### Data Augmentation
The dataset is augmented by adding the following transformations:
- Using the remaining part of the Wikipedia dataset
- Splitting longer sequnces (more than 16 words) into shorter ones

### Custom Loss Function
The loss function is a custom function which gives more importance to the first words of the sentence. 

### Translator
The Translator is defined as a Class. An object of this Class takes as input a batch of shuffled sentences and returns the reordered sentences. The inference phase is done by filtering the output of the model on the words presented in the input sentences.

### Beam Search
Another method used for the inference phase is the Beam Search. The Beam Search is implemented as a function which takes as input a batch of shuffled sentences and returns the reordered sentences. The Beam Search is used in the inference phase by filtering the output of the model on the words presented in the input sentences.

## Results
Using the provided scoring function, defined as the ratio between the longest common subsequence and the length of the longest sentence, we obtained a score of *0.605* on the test (over 3k samples) set using the Beam Search with a beam width of 4.