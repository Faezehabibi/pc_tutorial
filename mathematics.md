## Energy Function

In predictive coding networks, the network dynamics is defined by minimization 
of the total energy that is the result of the summation of the energy value over all layer.


$E = \sum_{i=0}^{L} E^{(i)} = \cdots + E^{(i)} + E^{(i-1)} + \cdots$

> This is equal to maximization of negative log likelihood of the multivariate gaussian
> distribution over the neural activities in each layer.


In the lens of energy-based models (EBM) [^longnote], energy function in predictive coding (a scalar value) is measures how much
the predicted value for neural activity in each layer fits to their actual activity. We can also rephrase the problem as finding 
a $\boldsymbol{\mu^l}$ that $\boldsymbol{E^l}~(\boldsymbol{\mu^l},\boldsymbol{z^l})$ is low for $\boldsymbol{z^l}$ and vice versa. [1]

[^longnote]: EBM says, given a pair of $(\boldsymbol{x}, \boldsymbol{y})$, 
return a scalar value that is called energy which indicates the compatibility of $\boldsymbol{y}$ with observed $\boldsymbol{x}$.


Each scalar indication layer's energy is the dot product of two vectors representing 
the "nerual activaty prediction error"  ($\mathbf{e}^l = (\mathbf{z}^l - \boldsymbol{\mu}^l)$) and 
the "activation mismatch" ($- \mathbf{e}^l = (\boldsymbol{\mu}^l - \mathbf{z}^l)$) at each layer. 

$E = \cdots + (\boldsymbol{e}^i)^T(\boldsymbol{e}^i) + (\boldsymbol{e}^{i+1})^T(\boldsymbol{e}^{i+1}) + \cdots$

Then the minimization problem for $E^i = (\boldsymbol{e}^i)^T(\boldsymbol{e}^i)$ becomes maximization problem for $-E^i = - (\boldsymbol{e}^i)^T (\boldsymbol{e}^i)$


There are other prospectives to it:
We can say that each layer's energy value is the energy averaged over two directional flow in the netwrok. At each layer $l$, 

$E^l = \frac{E^l_{\mu^l} + E^l_{z^l}}{2} = \frac{1}{2}(\boldsymbol{\mu}^i - \mathbf{z}^i)(\mathbf{z}^i - \boldsymbol{\mu}^i)^T + \frac{1}{2}(\mathbf{z}^i - \boldsymbol{\mu}^i)(\boldsymbol{\mu}^i - \mathbf{z}^i)^T$

> Note that inner product of two same dimensional vectors $\boldsymbol{x} \in R^d$ and  $\boldsymbol{y} \in R^d$ is their dot product in Euclidean space which results in
> a scalar value measuring two vectors alignment.
> $<\boldsymbol{x},\boldsymbol{y}> = \sqrt{\sum_{i=0}^{d} (x_i y_i)}$



$\mathbf{e}^i = (\mathbf{z}^i - \boldsymbol{\mu}^i)$ where dimensions are $(1,d) - (1,d)$

$E = \cdots + (\mathbf{z}^i - \boldsymbol{\mu}^i)^T(\mathbf{z}^i - \boldsymbol{\mu}^i) + (\mathbf{z}^{i+1} - \boldsymbol{\mu}^{i+1})^T(\mathbf{z}^{i+1} - \boldsymbol{\mu}^{i+1}) + \cdots$

$(\mathbf{z}^i - \boldsymbol{\mu}^i)^T(\boldsymbol{\mu}^i - \mathbf{z}^i) + (\boldsymbol{\mu}^i - \mathbf{z}^i)^T(\mathbf{z}^i - \boldsymbol{\mu}^i) + \cdots$

$\boldsymbol{\mu}^i = f(\mathbf{z}^{i-1})\mathbf{W}^{i-1}$ where dimensions are $(1,d) = (1,d') \cdot (d',d)$ and $\mathbf{W}^{i-1}$ is

$E = \cdots + (\mathbf{z}^i - f(\mathbf{z}^{i-1})\mathbf{W}^{i-1})^T(\mathbf{z}^i - f(\mathbf{z}^{i-1})\mathbf{W}^{i-1}) + (\mathbf{z}^{i+1} - f(\mathbf{z}^i)\mathbf{W}^i)^T(\mathbf{z}^{i+1} - f(\mathbf{z}^i)\mathbf{W}^i) + \cdots$

**Vector** 
**Scalar** 
**Matrix** 

$(1,d)$

### References

[1] https://atcold.github.io/NYU-DLSP20/en/week07/07-1/
