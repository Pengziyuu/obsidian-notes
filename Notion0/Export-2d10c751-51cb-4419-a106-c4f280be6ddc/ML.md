- **Regression**: The function outputs a **scalar**.

- **Classification**: The function outputs the **correct options (classes)**.

![[Attachments/image 9.png|image 9.png]]

---

# Regression

- **hyperparameters**: 事先給定的，用來控制學習過程的參數

## Training Step

### 1. Function with Unknown Parameters

- **Model (**$y = b + wx_1$**)**

- **feature (**$y$**、** $x_1$**)**

- **weight(**$w$**)**

- **bias (**$b$**)**

### 2. Define Loss from Training Data

$$Loss : L(b, w)=\frac1N\sum_n\;e^n$$

- **Loss (**$L(b,w)$: a function of parameters): how good a set of values (parameters) is.

- **Label (**$\widehat y$**)**: true value

- $e\;=\;\left|y-\widehat y\right|$ : L is the **mean absolute error (MAE)**

- $e\;=\;{(y-\widehat y)}^2$ : L is the **mean square error (MSE)**

![[Attachments/image 1 3.png|image 1 3.png]]

==**Error Surface:**== 把參數變化對**Loss變化作圖**

### 3. Optimization

$$w^\ast,\;b^\ast\;=\;arg\;\underset{w,b}{min}\;L$$

- **Gradient Descent: 找** $w^*,b^*$ **方法之一**
    
    1. (Randomly) Pick an initial value $𝑤^0,b^0$
    
    1. Compute
        
        $\frac{\operatorname{𝜕}\operatorname{𝐿}}{\operatorname{𝜕}\operatorname{𝑤}}\vert_{w=w^0,b=b^0} \\ \frac{\operatorname{𝜕}\operatorname{𝐿}}{\operatorname{𝜕}\operatorname{b}}\vert_{w=w^0,b=b^0}$
        
    
    3. Update 𝑤 iteratively
    
    $$w^1\leftarrow w^0-\operatorname{𝜂}\frac{\operatorname{𝜕}\operatorname{𝐿}}{\operatorname{𝜕}w}\vert_{w=w^0,b=b^0}  
    \\  
    b^1\leftarrow b^0-\operatorname{𝜂}\frac{\operatorname{𝜕}\operatorname{𝐿}}{\operatorname{𝜕}b}\vert_{w=w^0,b=b^0}$$
    
    **𝜂**: learning rate
    

---

## Activation function

![[Attachments/image 2 3.png|image 2 3.png]]

- **Linear**
    
    $$y=b+wx_1$$
    
    ![[Attachments/image 3 3.png|image 3 3.png]]
    
    ==Linear==
    

- **Sigmoid**
    
    $$y=c\frac1{1+e^{-(b+wx_1)}}  
    \\  
    =c\ sigmoid(b+wx_1)$$
    
    ![[Attachments/image 4 3.png|image 4 3.png]]
    
    ==Sigmoid==
    
    ![[Attachments/image 5 3.png|image 5 3.png]]
    
    ==Change w,b,c==
    
    **缺點：**
    
    - **梯度消失 (Vanishing Gradients)：** 當輸入值非常大或非常小時，函數的梯度（導數）會趨近於 0。在深度網路中，這會導致反向傳播時梯度不斷衰減，使得前面的網路層學習速度變得非常緩慢，甚至停止學習。
    
    - **輸出非以 0 為中心 (Not zero-centered)：** 輸出恆為正值，這會導致後續神經元的輸入都是正的，在反向傳播時可能導致權重更新方向的效率較低（產生 "zig-zagging" 現象）。
    
    - 計算成本較高（因為包含指數運算）。
    

- **ReLU (Rectified Linear Unit)**
    
    $$c\ max(0,b+wx_1)$$
    
    ![[Attachments/image 6 3.png|image 6 3.png]]
    
    ==**ReLU**==
    
    **缺點：**
    
    - **Dying ReLU 問題：** 如果一個神經元的輸入在訓練過程中始終為負，那麼它的輸出將永遠是 0，梯度也永遠是 0。這意味著這個神經元的權重將永遠不會被更新，這個神經元就「死亡」了。學習率 (learning rate) 設置過大時更容易出現此問題。
    
    - **輸出非以 0 為中心。**
    

### Sigmod Model

![[Attachments/image 7 2.png|image 7 2.png]]

---

![[Attachments/image 8 2.png|image 8 2.png]]

![[Attachments/image 9 2.png|image 9 2.png]]

![[image 10.png]]

---

![[image 11.png]]

![[image 12.png]]

---

![[image 13.png]]

![[image 14.png]]

---

![[image 15.png]]

---

![[image 16.png]]

==Optimization==

---

### ReLU Model

![[image 17.png]]

---

## DNN

---

![[image 18.png]]

---

## Training Skill

![[image 19.png]]

### **Model Bias**

- the model has severe limitation
    
    ![[image 20.png]]
    

---

### Optimization Issue

- Model Bias v.s. Optimization
    
    ![[d25b1723-08a0-40c8-9fc5-8352de4c352a.png]]
    

1. Start from shallower networks (or other models),  
    which are easier to optimize.

1. If deeper networks do not obtain smaller losses on  
    training data, then there is an optimization issue.

  

---

- Critical point (local minima、saddle point)

- Tayler Series Approximation
    
    ![[image 21.png]]
    
    ![[image 22.png]]
    
    ![[image 23.png]]
    
    ![[image 24.png]]
    
    ---
    

- Momentum

![[image 25.png]]

![[image 26.png]]

---

- Learning rate

![[image 27.png]]

![[image 28.png]]

- Root Mean Square

![[image 29.png]]

![[image 30.png]]

- RMSProp

![[image 31.png]]

![[image 32.png]]

- Adam
    
    ![[image 33.png]]
    

- Learning Rate Scheduling

![[image 34.png]]

![[image 35.png]]

---

- Batch
    
    ![[image 36.png]]
    
    - **update**: every time update parameters
    
    - **epoch**: see all the batches once
    

- Small v.s. Large
    
    ![[image 37.png]]
    
    ![[image 38.png]]
    
    ![[image 39.png]]
    

- Changing Error Surface
    
    ![[image 40.png]]
    

- Feature Normalization
    
    ![[image 41.png]]
    

![[image 42.png]]

![[image 43.png]]

- Batch normalization

![[image 44.png]]

![[image 45.png]]

### ==**Overfitting**==

- Better on training data, worse on unseen data
    
    ![[image 46.png]]
    
      
    

1. More training data

1. Data augmentation
    
    ![[image 47.png]]
    

1. constrained model
    
    - Fewer parameters, sharing parameters
    
    - Fewer features
    
    - Early stopping
    
    - Regularization
    
    - Dropout
    

### Bias-Complexity Trade-off

![[image 48.png]]

- Cross Validation
    
    ![[image 49.png]]
    
      
    

- N-fold Cross Validation
    
    ![[image 50.png]]
    

### Mismatch

Your training and testing data have different distributions. Be aware of how data is generated.

---

# Classification

- Regression

![[image 51.png]]

![[image 52.png]]

- Classification

![[image 53.png]]

![[image 54.png]]

- Soft-max
    
    ![[image 55.png]]
    

- Cross-entropy
    
    ![[image 56.png]]
    

- Cross entropy v.s. Mean Square Error (MSE) (Optimization)
    
    ![[image 57.png]]
    

---

# CNN

---

# Self-attention

---

# Transformer

---

# Generative Model

---

# BERT

---

# Auto-encoder

---

# Explainable AI

---

# Attack

---

# Adaptation

---

# Reinforcement Learning

---

# Network Compression

---

# Life-long Learning

---

# Meta-Learning

---