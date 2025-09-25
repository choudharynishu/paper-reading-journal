**Citation:** Ramachandran, Prajit et al. “Searching for Activation Functions.” 
ArXiv abs/1710.05941 (2018): n. pag.


This paper proposes an automated approach for designing and searching for activation functions. 
The authors start from the context that ReLU activation functions have been a breakthrough since Krizhevsky et al. 2012. 
ReLU functions addressed the problem of 'dying gradients', and even though they are not differentiable at $x=0$
they are used widely. 

Researchers have attempted to come up with new activation functions by designing them 
manually with desirable properties. These desirable properties are, 

1. Non-Linearity (without non-linearity a neural network would collapse into a linear function)
2. Differentiability (ReLU is not differentiable at zero)
3. Range/Output Behavior: Zero-centered outputs often help with faster convergence, as it reduces bias in weight updates.
4. Monotonicity: It helps in optimization by ensuring increasing input increases output (ReLU is monotonic for $x>0$)

Back to the paper, the authors propose a core unit composed of two unary functions and a binary function.
A unary function takes one scalar input value and gives one scalar output value. Examples include, $sin(x), exp(x), |x|,
x^2$, etc. While a binary function takes two inputs and given one output value, for example, $x_1+x_2$, $exp(-(x_1-x_2)^2)$, etc.

So, as one can imagine, a combination with some unary and binary functions can generate a large number of possibilities which
can be difficult to evaluate. For this, authors used a combination of exhaustive and reinforcement learning based search. 
For combinations which consist of only two unary functions and a binary function, authors have used an exhaustive approach where
authors try all possible combinations one-by-one on a "child network". Here, "child network", means any standard proven neural 
network architecture on a benchmark dataset to select the best performing activation function. The performance is validation accuracy. 

However, for multi-core component activation functions, an example of that would be, $x+exp(sin(x)⋅σ(x))$ (2 core components),
the number of possibilities can increase exponentially. So an exhaustive search in this case isn't possible, so authors 
opt for reinforcement learning approach. Specifically, authors used the RNN controller (Zoph & Le, 2016) with Policy Proximal 
Optimization (Schulman et al., 2017) using the exponential moving average of rewards as a baseline to reduce variance. 

Interesting insights from the paper:
1. "Complicated activation consistently underperformed simpler activation functions, potentially due to increased optimization 
difficulty"
2. Top performing activation functions consistently had pre-activation $x$ as one of the unary functions
3. Periodic functions such as $sin(x) and cos(x)$ regularly appeared as promising candidates
4. Functions that used division tended to perform poorly

The robustness of the top-performing activation functions was tested using ResNet-164 (RN) (He et al., 2016b), 
Wide ResNet 28-10(WRN) (Zagoruyko & Komodakis, 2016), DenseNet 100-12 (Huang et al., 2017) models. Of the two top-performing
activation functions from this exercise. One of these top performing functions was the *Swish* function, $x*σ(βx)$.
Depending on the value of $β$ the *Swish* function can act between a scaled linear function and ReLU. The most important 
aspect in which the *Swish* function differs from ReLU is the non-monotonic bump for $x<0$. 
