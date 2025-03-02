###### Tags- [[Machine-Learning]], [[Pytorch]]
##### Related topics [[Back Propogation]]

### Notes - 
Certainly! Let’s dive deeper into **automatic differentiation (AD)** and how **PyTorch** implements it. I’ll structure the notes in a way that’s easy to understand and revisit later.

---

### **Automatic Differentiation (AD)**

#### **1. What is Automatic Differentiation?**
- Automatic differentiation is a set of techniques to **compute gradients** of arbitrary arithmetic operations efficiently.
- It is **not** the same as numerical differentiation (finite differences) or symbolic differentiation (manipulating mathematical expressions).
- AD works by breaking down a computation into a series of elementary operations and applying the **chain rule** of calculus to compute gradients.

---

#### **2. Why is AD Important?**
- In machine learning and deep learning, gradients are essential for **optimization** (e.g., gradient descent).
- AD is **efficient** and **accurate**, making it ideal for computing gradients in complex models like neural networks.

---

#### **3. How AD Works**
AD computes gradients by traversing a **computational graph**:
1. **Forward Pass**: Compute the output of the function by evaluating the operations step by step.
2. **Backward Pass**: Compute gradients by applying the chain rule from the output back to the inputs.

---

#### **4. Two Modes of AD**
1. **Forward Accumulation**:
   - Computes gradients from inputs to outputs.
   - Suitable for functions with fewer inputs than outputs.
   - Example: For \( y = f(g(h(x))) \), compute \( \frac{du_1}{du_0} \), then \( \frac{du_2}{du_1} \), and so on.

2. **Reverse Accumulation (Backpropagation)**:
   - Computes gradients from outputs to inputs.
   - Suitable for functions with fewer outputs than inputs (common in neural networks).
   - Example: For \( y = f(g(h(x))) \), compute \( \frac{dy}{du_2} \), then \( \frac{du_2}{du_1} \), and so on.

---

### **How PyTorch Implements Automatic Differentiation**

#### **1. Computational Graph**
- PyTorch builds a **dynamic computational graph** during the forward pass.
- Each operation (e.g., addition, multiplication) is recorded as a node in the graph.
- Tensors in PyTorch have a `requires_grad` attribute. If `True`, PyTorch tracks operations on the tensor.

#### **2. Forward Pass**
- During the forward pass, PyTorch:
  - Computes the output of the function.
  - Records the operations in the computational graph.

#### **3. Backward Pass**
- During the backward pass, PyTorch:
  - Computes gradients using **reverse accumulation**.
  - Applies the chain rule to propagate gradients from the output back to the inputs.

#### **4. Key Components**
1. **`torch.Tensor`**:
   - Tensors have a `grad` attribute to store gradients.
   - The `requires_grad=True` flag enables gradient tracking.

2. **`torch.autograd`**:
   - The `autograd` module implements automatic differentiation.
   - It uses the computational graph to compute gradients.

3. **`backward()`**:
   - The `backward()` function triggers the backward pass.
   - It computes gradients and stores them in the `grad` attribute of the tensors.

#### **5. Example in PyTorch**
```python
import torch

# Define tensors with gradient tracking
x = torch.tensor(2.0, requires_grad=True)
y = torch.tensor(3.0, requires_grad=True)

# Define a computation
z = x * y + y**2

# Perform backward pass
z.backward()

# Access gradients
print(x.grad)  # Gradient of z w.r.t. x
print(y.grad)  # Gradient of z w.r.t. y
```

#### **6. Dynamic Computational Graph**
- PyTorch uses a **dynamic graph**, meaning the graph is rebuilt on every forward pass.
- This allows for flexibility, such as changing the model architecture during runtime.

#### **7. Efficiency in Reverse Accumulation**
- Reverse accumulation is more efficient for neural networks because:
  - It avoids redundant computations.
  - It is well-suited for functions with many parameters (inputs) and a single output (loss).

---

### **Key Takeaways**
- Automatic differentiation is a powerful technique for computing gradients efficiently.
- PyTorch implements AD using a **dynamic computational graph** and **reverse accumulation**.
- The `requires_grad` flag enables gradient tracking, and the `backward()` function computes gradients.
- Reverse accumulation is preferred in deep learning because it is efficient for functions with many inputs and a single output.

---

### **Summary Table**

| **Concept**               | **Description**                                                                 |
|---------------------------|---------------------------------------------------------------------------------|
| Forward Accumulation       | Computes gradients from inputs to outputs.                                      |
| Reverse Accumulation       | Computes gradients from outputs to inputs (used in backpropagation).           |
| Computational Graph        | Dynamic graph built during the forward pass to track operations.                |
| `requires_grad=True`       | Enables gradient tracking for tensors.                                          |
| `backward()`               | Triggers the backward pass to compute gradients.                                |
| Dynamic Graph              | Graph is rebuilt on every forward pass, allowing flexibility.                   |

---


#### Research Papers



#### YT links



#### Potential Project Ideas
