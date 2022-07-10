# Word Embeddings and Recurrent Neural Network

## Recurrent Neural Networks are commonly used in speech rocognition because it has an internal memory that keeps track of previous inputs adn temporal data, which all affects the subsequent prediction. In simpler words, every word in a sentence depends on each other, and when we are getting to the last words of a sentence, the result from the previous words still must be analyzed. It's important to note that traditional RNN models are very slow and training can be difficult, and more advanced models like LSTM are used for NLP. However, it's important to understand RNN first.

## Machines can only read numbers, which means we need to perform Word Embeddings. The first step is Tokenization, which is the prcoess of breaking down a text into a list of tokens. There are a couple of considerations during this process, including typos, stop words ("the", "a", "of", etc), and upper / lower case conversions. For example, "goooood" may be an verexaggerated version of "good" or "god" and not a typo, while "apple" is a fruit and "Apple" is a company. Tokenization may look easy, but there are a lot of work done during this process. The second step is to create a dictionary, where all the tokens are assigned to an index. It's important to note that this dictionary only keeps track of all the unique words in the text, not how many times each appeared. With this, we can use sequence of indexes to represent the text.
<img width="1266" alt="Screen Shot 2022-07-04 at 10 52 31 PM" src="https://user-images.githubusercontent.com/102645083/177258684-df8a2a60-959a-4d89-8839-3da9a12f2aad.png">

## The next step is to align the sequences of every text in a set to the same length, and we can do so by performing zero padding on short sequences or cutting out portions of long sequences. For example, if we have "This movie is great" and "I suggest not wasting your time watching this" and want the sequence length to be six, we can changed them to "null null this movie is great" and "not wasting your time watching this".
<img width="1282" alt="Screen Shot 2022-07-04 at 11 02 40 PM" src="https://user-images.githubusercontent.com/102645083/177260038-121a8dad-185d-4c21-9b81-e5f28b36c321.png">

## We then perform one-hot encoding on every word, which means if there are n amount of words, the one-hot vectors are n-dimensional.
<img width="1133" alt="Screen Shot 2022-07-05 at 12 25 24 AM" src="https://user-images.githubusercontent.com/102645083/177273002-18694bdd-3d00-49e4-9eec-958e7d975eb1.png">

## Since each word is represented by a ridiculously long matrix, we dimensionality reduce each word (from a 5000 x 1 to a 32 x 1 matrix in the movie review example).
<img width="750" alt="Screen Shot 2022-07-05 at 12 44 36 AM" src="https://user-images.githubusercontent.com/102645083/177276592-fdc18e50-0810-49ee-a205-a19d9de24c4f.png">
