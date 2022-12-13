- Day 1
    - Created a rought schedule for tasks to do
    - Set up the repo for experiments and results
    - Recreate the causal trace experiments in paper through the demo
    - I've come up with a toy experiment to run
        - Based on labelled examples of positive/negative sentiment statements, consider the language model's outputs after an input of "[positive/negative text] + '. My opinion is ...'"
        - Consider the interventions of corrupting the embeddings of [positive/negative text]
        - Consider effect on LM (language model) probabilities of replacing corrupted hidden states/MLPs/attentions with clean runs
        - Repeat this for a variety of models
        - Should be fairly straightforward to adapt the existing codebase to this experiment
    - Challenges:
        - The main challenge is to figuring out a way to extract the LM's sentiment on the input text. After a method for this is achieved, a causal mediation analysis style intervention can be carried out similarly to the paper
        - Require a dataset of labeled sentiments for text data
        - Sentiments are somewhat more elusive than just facts
        - The specificity and generalization of the edits measured in the paper provide additional evidence that the found parts of the LM store the fact in question. A similar analysis might be harder for sentiment analysis, since it isn't as clear how to appropriately generalize from a sentiment edit, or which statements should be considered 'far' from the original edit
    - TODO:
        - Understand specifics of the codebase 
        - Read the paper MEMIT
        - Write a summary of the paper in doc
        - Find an appropriate dataset for sentiments
        - Read about causal mediation analysis up to a working understanding
- Day 2
    - Goals:
        - Understand the code for ROME causal tracing
        - Find an appropriate sentiment dataset to represent interventions 
        - Implement basic running experiments
        - Understand why average indirect effect is used instead of average direct effect, paper mentions noisiness of results
    - Worked through the code for causal tracing, enough to be able to use it for the goal of locating sentiments
    - Understood distinctions between direct and indirect effects
    - Generated causal traces graphs over hidden state for a few simple reviews, where the effect was measured on probability of the next word after 'I believe the product is ' being 'good'.
    - Findings:
        - Causal trace of sentiment location is not as clear as for facts, not as clear a distinction between early and later sites. Indirect effect is not concentrated on the last last token of the review, but spread through the review, and even on word following the review text. 
        - Longer reviews take prohibitevely long to calculate trace for, order m^2 computationally if m is the length of input
- Day 3
    - Goals:
        - For tweet sentiment dataset, see how good a proxy P(good) is for ratings
        - Using P(good) as a proxy, generate a graphs over a variety of reviews
    




