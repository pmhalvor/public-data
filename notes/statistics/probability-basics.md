<script type="text/javascript" async
  src="https://cdnjs.cloudflare.com/ajax/libs/mathjax/2.7.7/MathJax.js?config=TeX-MML-AM_CHTML">
</script>

# Statistics - Probabillity Basics
## Joint and Conditional Probabilities, Bayes Theorem, CLT and LTP

Table of contents for notes on probability basics:
- [Joint Probability](probability-basics.md#joint-probability)
- [Conditional Probability](probability-basics.md#conditional-probability)
- [Bayes' Theorem](probability-basics.md#bayes-theorem)
- [Law of Total Probability](probability-basics.md#law-of-total-probability)
- [Central Limit Theorem](probability-basics.md#central-limit-theorem)

## Joint Probability

The probability of two events occurring simultaneously.
The events should be independent of each other, meaning that the occurrence of one event does not affect the probability of the other event occurring.

Mathematically, the joint probability of two events A and B is denoted as $P(A ∩ B)$ and is defined as:
$$
P(A \cap B) = P(A) \cdot P(B)
$$

A venn diagram is a useful way to visualize joint probability.
![Venn Diagram](https://upload.wikimedia.org/wikipedia/commons/thumb/9/99/Venn0001.svg/1200px-Venn0001.svg.png)
_(Image from [Wikipedia](https://en.wikipedia.org/wiki/Probability))_

Some examples of joint probability:
- The probability of rolling a 2 and a 3 on a pair of dice is $\frac{1}{36}$.
- The probability of drawing a 3 of hearts and a 4 of spades from a deck of cards is $\frac{1}{52} \cdot \frac{1}{51}$.
- The probability of a coin landing on heads and a die landing on 6 is $\frac{1}{2} \cdot \frac{1}{6}$.

When applied to NLP, joint probability would represent the chances of a sequence of words occurring together. Take for example the sentence "I love you". The joint probability of the words "I", "love", and "you" occurring together would be the ovefrall probability of the sentence occurring in your dataset.

A simple set-up here is to assign a word's probability of occuring as the number of times it shows up in a corpus divided by the total number of words in the corpus. For example, if the word "I" occurs 100 times in a corpus of 1000 words, then its probability of occurring is $\frac{100}{1000} = 0.1$. Then assume "love" occurs only 30 times, and "you" occurs 70 times. The joint probability of the sentence "I love you" showing up in the corpus is then $0.1 \cdot 0.03 \cdot 0.07 = 0.00021$. 

This is a very simple example, and could serve as a baseline for more complex models. For example, we could use a Markov model to predict the probability of a word occurring given the previous word. This would be a conditional probability, which we'll discuss next.


## Conditional Probability

The probability of an event occurring given that another event has already occurred.
Again, the events could dependent or independent of each other.
Unlike joint probability, the events are not necessarily occurring simultaneously.

Mathematically, the conditional probability of two events A and B is denoted as $P(A | B)$ and is defined as:
$$
P(A | B) = \frac{P(A \cap B)}{P(B)}
$$

A nice way to visualize conditional probability is with a tree diagram.
![Tree Diagram](https://upload.wikimedia.org/wikipedia/commons/thumb/9/9c/Probability_tree_diagram.svg/2560px-Probability_tree_diagram.svg.png)
_(Image from [Wikipedia](https://en.wikipedia.org/wiki/Conditional_probability))_

Some examples of conditional probability:
- The probability of rolling a 3 on a die given that the number is odd is $\frac{1}{3}$.
- The probability of drawing a 4 of spades from a deck of cards given that the card is a spade is $\frac{1}{13}$.
- The probability of a coin landing on heads given that a die lands on 6 is $\frac{1}{2}$.

When applied to NLP, conditional probability would represent the chances of a word occurring given the previous word. Take for example the sentence "I love you". The conditional probability of the word "love" occurring given that the word "I" has already occurred would be the probability of the word "love" occurring in the corpus after the word "I" has already occurred.
One way to find determine probability of word-pair occurances is to break the corpus into two-word tuples. 

For example, the sentence "I love you" would be broken into the tuples "I love" and "love you". Then the conditional probability of the word "love" occurring given that the word "I" has already occurred would be the number of times the tuple "I love" occurs in the corpus divided by the number of times the word "I" occurs in the corpus. So, following our example from above, if the word "I" occurs 100 times in a corpus of 1000 words, and the tuple "I love" occurs 20 times, then the conditional probability of the word "love" occurring given that the word "I" has already occurred is $\frac{20}{100} = 0.2$.


## Bayes' Theorem

Bayes' theorem describes the probability of an event, based on prior knowledge of conditions that might be related to the event. 
It is used to calculate posterior probabilities given prior probabilities.

While similar to a conditional probability, Bayes' theorem is more general.
I like to this of it as a mirrored conditional probability.

Mathematically, Bayes' theorem is defined as:
$$
P(A | B) = \frac{P(B | A) \cdot P(A)}{P(B)}
$$

<!-- I don't know of a good way to visualize this. Come back. -->

Some examples of Bayes' theorem:
- The probability of a person having a disease given that they tested positive for the disease is $\frac{P(positive | disease) \cdot P(disease)}{P(positive)}$.
- The probability of a user having an interest in topic X, given that they have an interest in topic Y, is $\frac{P(topic Y | topic X) \cdot P(topic X)}{P(topic Y)}$.


To apply Bayes' theorem to our previous example, we need to expand a bit on our problem. Now, we are trying to predict the probability of a setence being classified as positive given that it contains the word "love". We'll use the same corpus as before, but now we'll need to add "positive" or "negative" labels to each sentence. 

Assuming an 40/60 split of positive and negative sentences in the corpus, the probability of a sentence being positive is $P(positive) = 0.4$ and the probability of a sentence being negative is $P(negative) = 0.6$. The probability of a sentence containing the word "love" is $P(love) = 0.1$. 

The probability of a sentence containing the word "love" given that it is positive is $P(love | positive) = 0.2$. The probability of a sentence containing the word "love" given that it is negative is $P(love | negative) = 0.05$. 

The Bayes theorem then allows us to calculate the probability of a sentence being positive given that it contains the word "love".

Mathematically, this would look like:
$$
P(positive | love) = \frac{P(love | positive) \cdot P(positive)}{P(love)} = \frac{0.2 \cdot 0.4}{0.1} = 0.8
$$

<!-- This is not the best example, since we already have both sides of the data, but at least it shows the consistency of the theorem -->

On a small scale, these calculations are not very useful. However, when applied to large datasets, Bayes' theorem can be combined with the Central Limit Theorem to make predictions about the probability of _any_ sentence being positive given that it contains the word "love".


## Central Limit Theorem

The Cenntral Limit Theorem (CLT) states that the sampling distribution of the mean of any independent, random variable will be [normal](probability-distributions.md#normal) or nearly normal if the sample size is large enough.

The central limit theorem is important because it allows us to make inferences about a population given a sample of data. It is the basis for many statistical tests and calculations.

I found a nice visualization for this on GitHub (https://github.com/dfsnow/clt).
![Central Limit Theorem](https://raw.githubusercontent.com/dfsnow/clt/master/gifs/log.gif)

 <!-- 
It got late so I asked ChatGTP for help. While the following proof may be correct, I feel I would have a hard time reiterating it. So I'll commetn it out for now, and adapt it to more interpretable language later. 

Mathematically, the Central Limit Theorem can be expressed as follows:

Let $ X_1, X_2, ..., X_n$ be a sequence of independent and identically distributed random variables with mean $ \mu$ and standard deviation $ \sigma$. 
The sum (or average) of these random variables, denoted as $ S_n$ (or $ \bar{X}$ for the average), follows an approximate normal distribution as $ n$, the sample size, becomes sufficiently large. Specifically, as $ n$ approaches infinity, the distribution of $ S_n$ (or $ \bar{X}$) converges to a normal distribution with mean $ n\mu$ and variance $ n\sigma^2$.

Mathematically, this can be represented as:

$$ S_n = X_1 + X_2 + ... + X_n $$

For the sum, the mean is $ E[S_n] = n\mu$ and the variance is $ \text{Var}(S_n) = n\sigma^2$.

For the average ($ \bar{X}$), the mean is $ E[\bar{X}] = \mu$ and the variance is $ \text{Var}(\bar{X}) = \frac{\sigma^2}{n}$.

In summary, the CLT can be mathematically represented as the convergence of the distribution of $ S_n$ or $ \bar{X}$ to a normal distribution as the sample size $ n$ increases, regardless of the original distribution of the random variables $ X_1, X_2, ..., X_n$. -->

## Law of Total Probability

<!-- This responce was also generated by ChatGPT. I want to add my own notes from school later, but am ready to give up for the night -->
The law of total probability is a fundamental rule relating marginal probabilities to conditional probabilities. It expresses the total probability of an outcome which can be realized via several distinct events.

Specifically, it states that the probability of an event $A$ can be calculated by considering all possible ways $A$ can occur, weighted by the probabilities of these different scenarios. Mathematically, for a partition of the sample space into mutually exclusive events $B_1, B_2, ..., B_n$, the law of total probability is expressed as:

$$ P(A) = P(A \cap B_1) + P(A \cap B_2) + ... + P(A \cap B_n) $$

In simpler terms, to find the probability of event $A$, you consider all the distinct ways $A$ can happen through the individual scenarios ($B_1, B_2, ..., B_n$). You multiply the probability of each scenario ($P(A \cap B_i)$) by the probability of that scenario occurring ($P(B_i)$), and then sum up these probabilities for all scenarios.

This law is particularly useful when dealing with complex events that can occur through different possible conditions or scenarios. By breaking down the problem into mutually exclusive cases and accounting for all possible outcomes, the law of total probability provides a systematic way to calculate the overall probability of an event.


<!-- ## References -->
