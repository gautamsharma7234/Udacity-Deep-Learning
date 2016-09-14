# Q. What are the continuous bag of words and skip-gram architectures, in layman's terms?

Both architectures describe how the neural network "learns" the underlying word representations for each word. Since learning word representations is essentially unsupervised, you need some way to "create" labels to train the model. Skip-gram and CBOW are two ways of creating the "task" for the neural network -- you can think of this as the output layer of the neural network, where we create "labels" for the given input (which depends on the architecture).

For both descriptions below, we assume that the current word in a sentence is wiwi.

CBOW: The input to the model could be wi−2,wi−1,wi+1,wi+2wi−2,wi−1,wi+1,wi+2, the preceding and following words of the current word we are at. The output of the neural network will be wiwi. Hence you can think of the task as "predicting the word given its context"
Note that the number of words we use depends on your setting for the window size.

Skip-gram: The input to the model is wiwi, and the output could be wi−1,wi−2,wi+1,wi+2wi−1,wi−2,wi+1,wi+2. So the task here is "predicting the context given a word". Also, the context is not limited to its immediate context, training instances can be created by skipping a constant number of words in its context, so for example, wi−3,wi−4,wi+3,wi+4wi−3,wi−4,wi+3,wi+4, hence the name skip-gram.
Note that the window size determines how far forward and backward to look for context words to predict.

According to Mikolov:
Skip-gram: works well with small amount of the training data, represents well even rare words or phrases.
CBOW: several times faster to train than the skip-gram, slightly better accuracy for the frequent words
This can get even a bit more complicated if you consider that there are two different ways how to train the models: the normalized hierarchical softmax, and the un-normalized negative sampling. Both work quite differently.
which makes sense since with skip gram, you can create a lot more training instances from limited amount of data, and for CBOW, you will need more since you are conditioning on context, which can get exponentially huge.