Recurrent Neural Network

## Recurrent Neural Networks are commonly used in speech rocognition because it has an internal memory that keeps track of previous inputs adn temporal data, which all affects the subsequent prediction. In simpler words, every word in a sentence depends on each other, and when we are getting to the last words of a sentence, the result from the previous words still must be analyzed. It's important to note that traditional RNN models are very slow and training can be difficult, and more advanced models like LSTM are used for NLP. However, it's important to understand RNN first.

# Processing Categorical Features
## Numerical, binary, and categorical features often all show up in datasets. Numerical features like age, year, or height don't have to be converted because their most important characteristic is that they can be directly compared to each other, while binary features like head or tail can be easily replaced with 0 or 1. This leaves us with categorical features, and we need to find ways to convert them numerically so they can be computable by machine learning models, and there is really only one option. For example, we may think that different country names can be replaced with integers, such as ["China" = 1, "Japan" = 2, "India" = 3, etc]. However, we can't just say that India - Japan = China because 3 - 2 = 1. While that is logically correct on paper but incorrect in reality, a model may not process it correctly and will end up treating it as numerical features like age or height, and this is why we must apply one-hot encoding. China would be (1,0,0) in this case, while Japan and India are (0,1,0 and (0,0,1). There are also two scenarios where one-hot encoding wll simulously fit in: 1) Even if single integers could replace categorical features, there isn't a way for us to put China and Japan together ["age" = 20, "sex" = 1, "nationality" = (China, Japan)], because we can't add those integers together. We can simply represent that using one-hot encoding as (1,1,0) 2) If one sample of dataset is missing a country ["age" = 20, "sex" = 1, "nationality" = null], instead of leaving that empty after data-cleaning, we can just replace it with (0,0,0).

# Processing Text Data
## Machines can only read numbers, which means we need to perform Word Embeddings. The first step is Tokenization, which is the prcoess of breaking down a text into a list of tokens. There are a couple of considerations during this process, including typos, stop words ("the", "a", "of", etc), and upper / lower case conversions. For example, "goooood" may be an verexaggerated version of "good" or "god" and not a typo, while "apple" is a fruit and "Apple" is a company. If there are too many tokens, the ones with the least frequencies should be removed to reduce dimensonal complexity and speed up computation. Tokenization may look easy, but there are a lot of work done during this process. The second step is to create a dictionary, where all the remaining tokens are assigned to an index. It's important to note that this dictionary only keeps track of all the unique words in the text, not how many times each appeared. With this, we can use sequence of indexes to represent the text.
<img width="1266" alt="Screen Shot 2022-07-04 at 10 52 31 PM" src="https://user-images.githubusercontent.com/102645083/177258684-df8a2a60-959a-4d89-8839-3da9a12f2aad.png">

# Text to Sequence
## The next step is to align the sequences of every text in a set to the same length, and we can do so by performing zero padding on short sequences or cutting out portions of long sequences. For example, if we have "This movie is great" and "I suggest not wasting your time watching this" and want the sequence length to be six, we can changed them to "null null this movie is great" and "not wasting your time watching this".
<img width="1282" alt="Screen Shot 2022-07-04 at 11 02 40 PM" src="https://user-images.githubusercontent.com/102645083/177260038-121a8dad-185d-4c21-9b81-e5f28b36c321.png">

## We then perform one-hot encoding on every word, which means if there are n amount of words, the one-hot vectors are n-dimensional.
<img width="1133" alt="Screen Shot 2022-07-05 at 12 25 24 AM" src="https://user-images.githubusercontent.com/102645083/177273002-18694bdd-3d00-49e4-9eec-958e7d975eb1.png">

## Since each word is represented by a ridiculously long matrix, we dimensionality reduce each word (from a 5000 x 1 to a 32 x 1 matrix in the movie review example).
<img width="750" alt="Screen Shot 2022-07-05 at 12 44 36 AM" src="https://user-images.githubusercontent.com/102645083/177276592-fdc18e50-0810-49ee-a205-a19d9de24c4f.png">

## With Word Embeddings out of the way, we can now look into RNN models. Like mentioned earlier, RNN is a good way to model sequential data, which means its neural network will look slightly different that CNN's. Instead of loading in every single word at once (one to one), it only takes in one word at a time (many to one) just like how humans read. For every word, the RNN model performs word embedding on it and oit is represented by a dimension reduced matrix (32-D in this project). There are 32 initial weights that can be all zeros or random numbers in a range, and 32 neurons in each layer, which means each neuron takes in a a total of 64 inputs. They each then have one output, and the 32 outputs are now the new weights and are passed on to the next layer. The outputs of the final layer is then flattened into an equation and it goes through an activation function to become the result / prediction.
![Screen Shot 2022-07-10 at 3 10 21 PM](https://user-images.githubusercontent.com/102645083/178163841-018841e9-0a53-44bc-8d53-daa375d4a4a9.png)

## Back-Propogation for RNN is extremely complicated, and there are many separate topics associated with it. The first topic is Vanishing & Exploding Gradient, and here is an simple example: 1.01 to the power of 1,000 is around 20,959, while 0.99 to the power of 1,000 is around 0.00004. Because we know that finding the partial derivative in respect to a weight requires multiplying the partial derivatives of components that reside later in the network due to the chain rule, this product can be indefinitely long. We might never know what all these partial derivative values are equal to, so we might end up getting a near zero number or an indefinitely large value. Earlier weights are typically subjected to this problem, because the earlier it resides in the network, the more terms are going to be included in the product that calculates the gradient, and the more of these terms are less or more than one, the quicker the gradient is going to vanish or explode.

## Looking into the IMDB Movie Review project, the dataset has 50000 movie reviews that are labeled positive or negative, and half of them will be used for training and the other for testing.


