## Energy Function

In predictive coding networks, the network dynamics is defined by minimization 
of the total energy that is the result of the summation of the energy value over all layer.


$E = \sum_{l=0}^{L} E^{(l)} = \cdots + E^{(l)} + E^{(l-1)} + \cdots$

> This is equal to maximization of negative log likelihood of the multivariate gaussian
> distribution over the neural activities in each layer.


In the lens of energy-based models (EBM) [^longnote], energy function in predictive coding (a scalar value) is measures how much
the predicted value for neural activity in each layer fits to their actual activity. We can also rephrase the problem as finding 
a $\boldsymbol{\mu^l}$ that $\boldsymbol{E^l} = (\boldsymbol{\mu^l},\boldsymbol{z^l})$ is low for $\boldsymbol{z^l}$ and vice versa. [1]

[^longnote]: EBM says, given a pair of $(\boldsymbol{x}, \boldsymbol{y})$, 
return a scalar value that is called energy which indicates the compatibility of $\boldsymbol{y}$ with observed $\boldsymbol{x}$.


Each scalar indication layer's energy is the dot product of two vectors representing 
the "nerual activaty prediction error"  ($\mathbf{e}^l = (\mathbf{z}^l - \boldsymbol{\mu}^l)$) and 
the "activation mismatch" ( $-\boldsymbol{e}^{(l)} =  \boldsymbol{\mu}^{(l)} - \mathbf{z}^{(l)}$ ) at each layer. 

$\boldsymbol{e}^l = (\boldsymbol{z}^l - \boldsymbol{\mu}^l)$

$E = \cdots + \boldsymbol{e}^{(l)^T} \boldsymbol{e}^{(l)} + \boldsymbol{e}^{(l-1)^T} \boldsymbol{e}^{(l-1)} + \cdots$

Then the minimization problem for $E^i = (\boldsymbol{e}^l)^T(\boldsymbol{e}^l)$ becomes maximization problem for $-E^l = - (\boldsymbol{e}^l)^T (\boldsymbol{e}^l)$

$E = \cdots + (\mathbf{z}^i - \boldsymbol{\mu}^i)^T(\mathbf{z}^i - \boldsymbol{\mu}^i) + (\mathbf{z}^{l-1} - \boldsymbol{\mu}^{l-1})^T(\mathbf{z}^{l-1} - \boldsymbol{\mu}^{l-1}) + \cdots$







> Note that inner product of two same dimensional vectors $\boldsymbol{x} \in R^d$ and  $\boldsymbol{y} \in R^d$ is their dot product in Euclidean space which results in
> a scalar value measuring two vectors alignment.
> 
> $<\boldsymbol{x},\boldsymbol{y}> = \sqrt{\sum_{i=0}^{d} (x_i y_i)}$




$\boldsymbol{\mu}^i = f(\mathbf{z}^{i-1})\mathbf{W}^{i-1}$

$E = \cdots + (\mathbf{z}^i - f(\mathbf{z}^{i-1})\mathbf{W}^{i-1})^T(\mathbf{z}^i - f(\mathbf{z}^{i-1})\mathbf{W}^{i-1}) + (\mathbf{z}^{i+1} - f(\mathbf{z}^i)\mathbf{W}^i)^T(\mathbf{z}^{i+1} - f(\mathbf{z}^i)\mathbf{W}^i) + \cdots$

**Vector** 
**Scalar** 
**Matrix** 

$(1,d)$

### References

[1] https://atcold.github.io/NYU-DLSP20/en/week07/07-1/
