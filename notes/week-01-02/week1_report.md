# Week 1-2 Concept Writeup

## JEPA

JEPA (Joint Embedding Predictive Architecture) is a representation learning framework proposed by Yann LeCun. Instead of predicting raw pixels or tokens, JEPA predicts a target embedding from a context embedding. The idea is that many details in the world are unpredictable, such as texture noise, exact lighting conditions, or the precise position of every leaf in a tree. Predicting all pixels forces a model to spend capacity on details that may not be useful for understanding the world.

A JEPA model contains an encoder, a predictor, and a target representation. The encoder converts inputs into embeddings. The predictor tries to predict the target embedding from the context embedding. The loss is applied in latent space rather than pixel space. According to LeCun, this allows the model to focus on high-level semantic information instead of wasting effort on unpredictable details.

One criticism of JEPA is that many of its long-term claims are still speculative. While the idea is promising, it is not yet clear whether latent-space prediction alone can lead to general intelligence or advanced reasoning abilities.

What I still do not fully understand: how JEPA can be extended from representation learning to long-horizon planning and reasoning.

## VICReg

VICReg (Variance-Invariance-Covariance Regularization) is a self-supervised learning method that learns useful representations without using labels. Two augmented views of the same image are generated and passed through an encoder and projector network. The resulting embeddings are trained using three different objectives.

The invariance term forces embeddings from two views of the same image to be similar. Without this term, the model would not learn view-invariant features.

The variance term prevents representational collapse by ensuring that each embedding dimension has enough variation across a batch. If this term is removed, the model can map all images to nearly identical embeddings.

The covariance term reduces redundancy by encouraging different embedding dimensions to capture different information. Without it, many dimensions may learn similar features and waste representational capacity.

Together these three terms produce embeddings that are stable, diverse, and informative. In my implementation, the learned embeddings achieved approximately 46.9% linear probe accuracy on CIFAR-10.

What I still do not fully understand: why the standard VICReg hyperparameters work well across many different datasets.

## Collocation-Based Planning

Collocation-based planning is a trajectory optimization method commonly used in robotics and control. Instead of simulating a system forward from an initial state, collocation treats the states and control inputs at multiple time points as optimization variables.

The decision variables are therefore the states and controls throughout the trajectory. Constraints are added to ensure that the trajectory satisfies system dynamics and task requirements such as velocity limits, acceleration limits, or obstacle avoidance.

One advantage of collocation is that all time steps are optimized simultaneously. This often makes it more stable than shooting methods, which can accumulate errors during forward simulation. Because constraints are enforced throughout the trajectory, collocation is frequently used in robotics and motion planning problems.

A disadvantage is that collocation can become computationally expensive when the system is large or when a very fine discretization is required. Choosing appropriate collocation points can also be difficult.

What I still do not fully understand: how practitioners choose collocation schemes for large real-world planning problems.
