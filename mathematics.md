## Energy Function

In predictive coding networks, the network dynamics is defined by minimization 
of the total energy that is the result of the summation of the energy value over all layer.


$E = \sum_{i=0}^{L} E^i = \cdots + E^i + E^{i-1} + \cdots$

> This is equal to maximization of negative log likelihood of the multivariate gaussian
> distribution over the neural activities in each layer.

In the lens of energy-based models (EBM) which says, given a pair of $(\boldsymbol{x}, \boldsymbol{y})$, 
return a scalar value that is called energy which indicates the compatibility of $\boldsymbol{y}$ with observed $\boldsymbol{x}$.

energy function in predictive coding (a scalar value) is calculated by 

dot product of two vectors representing the prediction error and the "activation mismatch" at each layer. 

$(\mathbf{z}^i - \boldsymbol{\mu}^i)^T(\boldsymbol{\mu}^i - \mathbf{z}^i) + (\boldsymbol{\mu}^i - \mathbf{z}^i)^T(\mathbf{z}^i - \boldsymbol{\mu}^i)$

$E^i = (\mathbf{e}^i)^T(\mathbf{e}^i)$ where $\mathbf{e}^i$ 

$E = \cdots + (\mathbf{e}^i)^T(\mathbf{e}^i) + (\mathbf{e}^{i+1})^T(\mathbf{e}^{i+1}) + \cdots$

$\mathbf{e}^i = (\mathbf{z}^i - \boldsymbol{\mu}^i)$ where dimensions are $(1,d) - (1,d)$

$E = \cdots + (\mathbf{z}^i - \boldsymbol{\mu}^i)^T(\mathbf{z}^i - \boldsymbol{\mu}^i) + (\mathbf{z}^{i+1} - \boldsymbol{\mu}^{i+1})^T(\mathbf{z}^{i+1} - \boldsymbol{\mu}^{i+1}) + \cdots$

$(\mathbf{z}^i - \boldsymbol{\mu}^i)^T(\boldsymbol{\mu}^i - \mathbf{z}^i) + (\boldsymbol{\mu}^i - \mathbf{z}^i)^T(\mathbf{z}^i - \boldsymbol{\mu}^i) + \cdots$

$\boldsymbol{\mu}^i = f(\mathbf{z}^{i-1})\mathbf{W}^{i-1}$ where dimensions are $(1,d) = (1,d') \cdot (d',d)$ and $\mathbf{W}^{i-1}$ is

$E = \cdots + (\mathbf{z}^i - f(\mathbf{z}^{i-1})\mathbf{W}^{i-1})^T(\mathbf{z}^i - f(\mathbf{z}^{i-1})\mathbf{W}^{i-1}) + (\mathbf{z}^{i+1} - f(\mathbf{z}^i)\mathbf{W}^i)^T(\mathbf{z}^{i+1} - f(\mathbf{z}^i)\mathbf{W}^i) + \cdots$

**Vector** 
**Scalar** 
**Matrix** 

$(1,d)$
