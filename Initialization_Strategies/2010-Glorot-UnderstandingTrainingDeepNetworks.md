**Citation:**  
Glorot, Xavier and Yoshua Bengio. “Understanding the difficulty of training deep feedforward neural networks.” 
International Conference on Artificial Intelligence and Statistics (2010).
---

## 1. Motivation
- Prior work (LeCun et al., 1998) identified issues with the sigmoid activation function 
(non–zero-centered outputs, saturation).
- Understand the limitations of random initialization for training Deep Neural Network
- Proposed a new normalized initialization scheme that balances variance of activations and gradients
for effective training
---

## 2. Key Contributions
- Systematic empirical evaluation of activation functions (Sigmoid, Tanh, Softsign) across multiple datasets.
- Demonstrated that random initialization with sigmoid leads to saturation in upper layers and weak gradients
for lower layers.
- Theoretical variance analysis for forward and backward passes → identified conditions for stable gradient propagation.
- Proposed a normalized initialization scheme to balance forward and backward variance, mitigating vanishing gradients.
---

## 3. Method / Experiment Setup
- Experiments on Shapeset, MNIST, CIFAR-10, and ImageNet.
- Architecture: feedforward networks with 1–5 layers, 1000 hidden units per layer.
- Training setup:
  - Softmax logistic regression output 
  - Negative log-likelihood cost function 
  - Hyperparameters: learning rate, number of layers 
  - Initialization: “Efficient Backprop” (LeCun et al., 1998)
- Theoretical derivation:
  - To maintain variance in forward pass → weight variance ∝ 1/hidden size 
  - To maintain variance in backward pass → weight variance ∝ 1/output size
  - Normalized initialization balances both conditions.
---

## 4. Results / Findings
- Sigmoid:
  - Rapid saturation, especially in upper layers. 
  - Random initialization pushes hidden outputs toward zero → very small gradients in lower layers 
- Tanh:
  - Saturation happens more gradually, layer by layer.
- Softsign:
  - Initially saturates faster, but then stabilizes → better empirical performance.
- Proposed initialization scheme:
  - Prevented gradients from vanishing as quickly. 
  - Gradient variance remained constant across layers, even when magnitudes decreased
---

## 6. Limitations / Open Questions
- Limited set of activation functions (e.g., no ReLU, which later became dominant). 
- Experiments constrained to moderate depths (1–5 layers), less representative of modern very deep networks
---



