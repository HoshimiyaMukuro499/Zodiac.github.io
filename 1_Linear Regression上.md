Compiled by xyt、生命科学学院
说明：本笔记以吴恩达《机器学习》的课程内容为基础，对于可能的缺误与遗漏进行改正与修补，以期能够在他人学习《机器学习》课程时起到纲要或讲义的作用。个人编写，错误在所难免，欢迎在github上提出pull request。
## 机器学习的定义

Machine Learning is field of study that gives computers **the ability to learn** without being explicitly programmed.

根据类型，可以粗略的分为Supervised Learning监督学习，Unsupervised Learning非监督学习，Recommender Systems推荐系统，Reinforced Learning强化学习等。

# Part One: Supervised Learning

机器学习的目的是能够从给定的input$X$得出正确的output$Y$。而在训练集中给定$X$以及正确答案$Y$的学习算法为**监督学习**。

## Regression 回归

Predict a number from **infinitely** possible outputs.

### Basic Terminology 基本术语

**Training set**: Data used to train the model
x : **"input" variable/feature**
y : **"output" variable/"target"variable**
**m** : number of training examples
**(x,y)** : single training example
$(x^{(i)},y^{(i)})$:the ith training example(i=1,2,3...)
$$x \xrightarrow{f} \hat y$$ f is composed of **training set** and **learning algorithm**.

对于输入变量只有一个的线性回归模型$f_{w,b}(x)=wx+b$
我们称之为**Univariate** linear regression单变量线性回归。

### Cost function

对于每一次预测，有$$\hat y^{(i)} = f_{w,b}(x^{(i)})=w \cdot x^{(i)} + b $$
我们想要Find w,b such that $\hat y^{(i)}$ is very close to $y^{(i)}$ for all $(x^{(i)},y^{(i)})$
在线性回归中，我们用**均方差损失函数**（Squared error cost function）去描述y_hat与y的偏差。
$$J(w,b)=\frac {1}{2m} \sum_{i=1}^{m}(\hat y^{(i)}-y^{(i)})^2$$
或写作
$$J(w,b)=\frac {1}{2m} \sum_{i=1}^{m}(f_{w,b}(x^{(i)})-y^{(i)})^2$$


### Gradient Descent

我们的目标是找到w,b能够最小化损失函数$J(w,b)$,然而多数情况下，让计算机一步到位地找到函数的最小值是不容易的。因此，我们使用以下**梯度下降**思想：

- Start with some w,b
- Keep changing w,b to reduce $J(w,b)$
- Until we settle at or near a minimum.

值得注意的是，这样梯度下降所达到的最小值为**Local minimal** 局部最小值而非全局最小值。因此，根据回归函数的不同，适当地选取损失函数使得梯度下降达到的局部最小值即是全局最小值是必要的。

### Implementing Gradient Descent

为了实现Keep changing w,b to reduce $J(w,b)$，我们定义以下的变化方式：
$$w = w - \alpha \frac{\partial J}{\partial w}$$$$b = b - \alpha \frac{\partial J}{\partial b}$$
repeat until **convergence**.(这里吴恩达对于convergence的描述是w,b do not change much,当然这可以被更严谨地从数学上定义)

在计算机实现时，需要注意**Simutaneously update w and b** 同步更新w,b，以免由于w的改变而影响$\frac{\partial J}{\partial b}$项。

```text
temp_w = w - alpha * d/dw * J
temp_b = b - alpha * d/db * J
w=temp_w
b=temp_b
```

### Learning rate

$\alpha$ 为**学习率**
If $\alpha$ is too small:
- Gradient descent may be slow.
If $\alpha$ is too big:
- **Overshoot**, never reach minimum
- Fail to converge, diverge instead.

在梯度下降中，**Overshoot（过冲）** 指的是参数更新时“一步迈得太大”，直接跨过了最优点，跑到另一侧去的现象。

不加证明地给出：**J can reach local minimum with fixed learning rate.**

>在补充资料中给出AI生成的论证，以作参考。

### Gradient descent for Linear regression

将均方差损失带入$\frac{\partial J}{\partial w}$与$\frac{\partial J}{\partial b}$中，得到
$$ w= w - \alpha \frac {1}{m} \sum_{i=1}^{m}(f_{w,b}(x^{(i)}-y^{(i)})\cdot x^{(i)})$$
$$ b= b - \alpha \frac {1}{m} \sum_{i=1}^{m}(f_{w,b}(x^{(i)}-y^{(i)}))$$

不加证明地给出：**均方差损失函数是凸(convex)的，因此梯度下降可以达到全局最小值。**

**Batch gradient descent**: Each step of gradient descent uses all the training examples.
