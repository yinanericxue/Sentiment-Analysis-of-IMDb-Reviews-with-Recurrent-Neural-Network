# Word Embeddings and Recurrent Neural Network

## In this project, there will be 50,000 total movie reviews that are labeled with either "positive" or "negative", and half of them are used for training while the other half is used for testing. 

## The first step is to perform Tokenization, the prcoess of breaking down a text into a list of tokens. There are a couple of considerations during this process, including typos, stop words ("the", "a", "of", etc), and upper / lower case conversions. For example, "goooood" may be an verexaggerated version of "good" or "god", while "apple" is a fruit and "Apple" is a company. Tokenization may look easy, but there are a lot of work done during this process. The second step is to create a dictionary, where all the tokens are assigned to an index. It's important to note that this dictionary only keeps track of all the unique words in the text, not how many times each appeared. With this, we can use sequence of indexes to represent the text.
<img width="1266" alt="Screen Shot 2022-07-04 at 10 52 31 PM" src="https://user-images.githubusercontent.com/102645083/177258684-df8a2a60-959a-4d89-8839-3da9a12f2aad.png">

## The next step is to align the sequences of every movie review text to the same length, and we can do so by performing zero padding on short sequences or cutting out portions of long sequences. For example, if we have "This movie is great" and "I suggest not wasting your time watching this" and want the sequence length to be six, we can changed them to "null null this movie is great" and "not wasting your time watching this".
<img width="1282" alt="Screen Shot 2022-07-04 at 11 02 40 PM" src="https://user-images.githubusercontent.com/102645083/177260038-121a8dad-185d-4c21-9b81-e5f28b36c321.png">

## We then perform one-hot encoding on every word, which means if there are n amount of words, the one-hot vectors are n-dimensional.
<img width="1133" alt="Screen Shot 2022-07-05 at 12 25 24 AM" src="https://user-images.githubusercontent.com/102645083/177273002-18694bdd-3d00-49e4-9eec-958e7d975eb1.png">

## Using all the vectors
<img width="750" alt="Screen Shot 2022-07-05 at 12 44 36 AM" src="https://user-images.githubusercontent.com/102645083/177276592-fdc18e50-0810-49ee-a205-a19d9de24c4f.png">
