# [Paper Summary] LEARNING TO ADAPT IN DYNAMIC, REAL-WORLD ENVIRONMENTS THROUGH META-REINFORCEMENT LEARNING
## Motivation
- Generating samples is exceedingly expensive.
- Unexpected perturbations or unseen situations cause proficient but specialized policies to fail at test time.
- The central challenge of MBRL is acquiring an accurate global model throughout the entire state space.
- The dynamics inherently change as a function of uncontrollable and often unobservable environment factors.

## Meta-Learning
Meta-learning has the following 5 ingredients:
A task distribution p(T).
For each task, we have loss L(T), training dataset
