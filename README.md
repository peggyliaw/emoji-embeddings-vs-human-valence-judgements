# emoji-embeddings-vs-human-valence-judgements
This is a summary of the project. Detailed project documentation can be found in the pdf in this repository: Evaluating emoji semantics.
## Background
Emojis have been widely used across online communications such as social media posts, text messages, video comments etc. With its prevalence, emojis are used in a similar way as natural languages (i.e., words) for expressing thoughts and ideas. However, while researchers in natural language processing have developed methods to quantitatively assess words' meanings and how they are used in various contexts, our understandings of the semantics of emojis remains limited.

One way to evaluate words is creating embedding space where the distance between two word vectors (calculated by cosine similarity) represents how similar the two words are to each other, one can also evaluate meanings in emojis using the same method. There has been work on creating embedding spaces for emojis, such as emoji2vec and emojional. These researchers mathematically appended emojis into the word2vec embedding space based on the contexts that the emojis appear in. This technique allows each emoji to have its own vector for quantitative assessments.

The availability of emoji embedding spaces raises a question - do these mathematical frameworks to quantify emojis mirror humans' understandings of emojis? To answer this question, we evaluated emotional valence (i.e., positive, neutral, or negative feelings associated with a stimulus) between embedding spaces (i.e., emoji2vec and emojional) and human ratings.

## Analyses and Results
Below is a list of datasets used in the analyses:

- Emoji2vec: https://arxiv.org/abs/1609.08359
- Emojional: https://doi.org/10.1007/978-3-030-87094-2_27
- Human ratings: https://doi.org/10.1371/journal.pone.0144296

We appended emoji embedding vectors to human ratings, which were treated as the target for classifications. Next, we trained 3 classification models, Support Vector Machine, Random Forest, and XGBoost, using the embedding vectors. Performance was evaluated using accuracy and F1 scores, and we used bootstrapping to generate confidence intervals for statistical comparisons.

Since the sample sizes in each class were imbalanced, we implemented SMOTE (i.e., Synthetic Minority Over-sampling Technique) and downsampling to bring 3 classes to have equal number of samples. While class balancing helped improve model performances across all 3 models, Random Forest especially benefited from this step. The improvements were observed in neutral and negative classes on the expense of positive class.

Overall, emoji2vec and emojional had similar performance in classifying emojis into positive, neutral, or negative class. When comparing the three classifiers trained on imbalanced datasets, Support Vector Machine and XGBoost had similar level of performance, followed by Random Forest. In contrast, after class balancing, Random Forest had significant improvement and had a similar level of performance to Support Vector Machine and Random Forest.

## Implications
While emoji2vec and emojional demonstrated that embedding spaces can capture emotional valence, their modest accuracy (50–60%) reveals a gap between vector representations and human interpretation. This suggests that current embeddings fail to fully account for the polysemous and context-dependent nature of emoji semantics.

Since this project worked with raw 300-dimensional vectors, performances from classifiers may not be optimized as information is sparse. Future work can Perform feature engineering in embedding vectors to bring 300-dimensions down to a more manageable number that can be directly mapped to semantic information.

There has been work on understanding the meanings of higher order dimensions in word2vec (https://doi.org/10.3758/s13423-024-02551-y) and categorizing metaphors using word2vec ( https://doi.org/10.3758/s13428-021-01558-w). Here is another paper on interpretability of word embeddings (https://arxiv.org/pdf/1711.00331).
