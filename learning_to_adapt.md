# [Paper Summary] LEARNING TO ADAPT IN DYNAMIC, REAL-WORLD ENVIRONMENTS THROUGH META-REINFORCEMENT LEARNING
## Motivation
- Generating samples is exceedingly expensive.
- Unexpected perturbations or unseen situations cause proficient but specialized policies to fail at test time.
- The central challenge of MBRL is acquiring an accurate global model throughout the entire state space.
- The dynamics inherently change as a function of uncontrollable and often unobservable environment factors.

## Meta-Learning
Meta-learning has the following 3 ingredients:

- A task distribution $\rho(\mathcal{T})$. 
- For each task, we have loss $\mathcal{L}_{\mathcal{T}}$, training dataset $\mathcal{D}^{tr}_{\mathcal{T}}$, testing data set $\mathcal{D}^{test}_{\mathcal{T}}$.
- A parameterized learning procedure $u_{\psi}$ that maps meta model parameter $\theta$ to specific model parameter $\theta'$ as $\theta'=u_{\psi}(\mathcal{D}^{tr}_{\mathcal{T}}, \theta)$. 

The objective of meta learning is 
$$
\min_{\theta,\psi}\mathbb{E}_{\mathcal{T}\sim\rho(\mathcal{T})}[\mathcal{L}(\mathcal{D}^{\text{test}}_{\mathcal{T}}, \theta')], \quad \text{s.t.} \quad \theta'=u_{\psi}(\mathcal{D}^{tr}_{\mathcal{T}}, \theta)
$$
where the meta-learner tries to find model parameter and adapt parameter such that by training on few examples, it can perform well on test data. Moreover, it has the potential to generalize to unseen tasks.

### Gradient-based meta-learning

Model-agnostic meta-learning (MAML) (Finn et al., 2017) aims to learn initialization parameters of a neural network such that taking one or several gradient descent steps from this initialization leads to effective generalization (or few-shot generalization) to new tasks. The adaptation procedure of MAML is $u_{\psi}(\mathcal{D}^{tr}_{\mathcal{T}}, \theta)=\theta-\alpha\nabla_{\theta}\mathcal{L}(\mathcal{D}^{tr}_{\mathcal{T}},\theta)$.

### Recurrence-based meta-learning

In recurrent models such as LSTM and GRU, we have input $x_t$, hidden state $h_t$ and output $y_t$. For recurrence-based meta-learning, the input $x_t$ is the training data, $h_0$ is the initial model parameter. The resulting hidden state is treated as adapted model parameter $\theta'$. It is then served as local dynamics model to perform MPC.

## Meta-Learning for Online Model Adaptation

The core idea of meta-learning for online model adapation is

- Learn meta-dynamics model to alleviate the sample complexity of model-free algorithms
- Use the previous *M* steps to perform local model update and test on the *K* steps afterwards
- Update model parameter $\theta$ and adaptation paratemer $\psi$ every $n_S$ steps

## Discussions

- This approach avoids training a global accurate dynamics model by using online adapation.
- The drawback of this approach is the temporal correlation of dynamics assumption. For example, there may be a sudden change of the dynamics model, but may resemble transitions long time ago. This can be solved by incorporating a mixture of dynamics models.
- This paper is very well written. The language from the introduction and related work section can be borrowed from.