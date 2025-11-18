# RGC to PC

<img src="images/PC_brain.jpeg"/>






pre: [Information Flow](https://github.com/Faezehabibi/pc_tutorial/blob/19b0692fa307f2b06676ca93b9b93ba3ba854766/information_flow.md)

## What we knew before predictive coding?

### Retina
Last stage in retina, Retinal Ganglion Cells (RGCs), spatially reduces redundancy in sensory input while Lateral Geniculate Nucleus (LGN) reduces redundant information in the time domain.
Retina spot process the sensory input in a small pathches processed in local in lowest level. Connecting these local patched areas the lines line dot
And with the lines you can make a scene
Your retina has lots of units responsible for processing small patches of the visual data
I it starts by dots

### Orientation Selective Responde
Simple cells in Hubble and Wiesel Experiment 1962

### End-stopped
Extra-classical receptive fields (Contextual Modulation and Surround Suppression) effects clue that the brain is using efficient coding (redundancy reduction).
To investigate whether some of these effects could 
result from the extended positive correlations along 
dominant orientation directions in natural images, 

### Sparcse Coding (1996)
Showed Orientation Selective Responde of simple cells


-----------------------------------------------------------------------------------------------------

# Predictive Coding (1999)


## Predictive Coding with NGC-Learn
-----------------------------------------------------------------------------------------------------

### PC model for Reconstruction Task

<!-- Autoencoder -->





#### Build PC model

##### Make Component:

###### 1- Make Neural component:


**Responding Neurons**
<br>

We want to build a hierarchical neural network we need neural layers. In predictive coding network with real-valued dynamics
we use `RateCell` components ([RateCell tutorial](https://ngc-learn.readthedocs.io/en/latest/tutorials/neurocog/rate_cell.html)).
Here, we want 3-layer network (3-hidden layers) so we define 3 components, each with `n_units` size for hidden representatins.

```python
z3 = RateCell("z3", n_units=h3_dim, tau_m=tau_m, act_fx=act_fx, prior=(prior_type, lmbda))
z2 = RateCell("z2", n_units=h2_dim, tau_m=tau_m, act_fx=act_fx, prior=(prior_type, lmbda))
z1 = RateCell("z1", n_units=h1_dim, tau_m=tau_m, act_fx=act_fx, prior=(prior_type, lmbda))
```




<!-- ################################################################################ -->

<br>
<br>

<img src="images/GEC.png" width="120" align="right"/>

**Error Neurons**
<br>


For each activation layer we have a set of additional neurons with the same size to measure the prediction error for individual 
`RateCell` components. The error value will later be used to calculate the **energy** for layers (including hiddens) and the whole model.


```python
e2 = GaussianErrorCell("e2", n_units=h2_dim)          ## e2_size == z2_size
e1 = GaussianErrorCell("e1", n_units=h1_dim)          ## e1_size == z1_size
e0 = GaussianErrorCell("e0", n_units=in_dim)          ## e0_size == z0_size (x size)
```

<!-- ################################################################################ -->

###### 2- Make Synaptic component:

<!-- ################################################################################ -->

<br>
<br>

<!-- <img src="images/GEC.png" width="120" align="right"/> -->

**Forward Synapses**
<br>

To connect layers to each others we create synapstic components. To send infromation in forward pass (from input into deeper layers with a bottom-up stream) 
we use `ForwardSynapse` components. Check out [Brain's Information Flow](https://github.com/Faezehabibi/pc_tutorial/blob/main/information_flow.md#---information-flow-in-the-brain--)
for detailed explanation of information flow in brain modeling.


```python
E3 = ForwardSynapse("E3", shape=(h2_dim, h3_dim))          ## pre-layer size  (x) => (h1) post-layer size
E2 = ForwardSynapse("E2", shape=(h1_dim, h2_dim))          ## pre-layer size (h1) => (h2) post-layer size
E1 = ForwardSynapse("E1", shape=(in_dim, h1_dim))          ## pre-layer size (h2) => (h3) post-layer size
```

<!-- ################################################################################ -->

<br>
<br>

<!-- <img src="images/GEC.png" width="120" align="right"/> -->

**Backward Synapses**
<br>

For each `ForwardSynapse` components sending infromation upward (bottom-up stream) exist a `BackwardSynapse` component to reverse the information flow and 
send it back downward (top-down stream -- from top layer to bottom/input). If you are not convinced, check out [Information Flow](https://github.com/Faezehabibi/pc_tutorial/blob/19b0692fa307f2b06676ca93b9b93ba3ba854766/information_flow.md).

```python
W3 = BackwardSynapse("W3",
                     shape=(h3_dim, h2_dim),          ## pre-layer size (h3) => (h2) post-layer size
                     optim_type=opt_type,             ## optimization method (sgd, adam, ...)
                     weight_init=w3_init,             ## W3[t0]: initial values before training at time[t0]
                     w_bound=w_bound,                 ## -1 for deactivating the bouding synaptic value
                     sign_value=-1.,                  ## -1 means M-step solve minimization problem
                     eta=eta,                         ## learning-rate (lr)
)
W2 = BackwardSynapse("W2",
                     shape=(h2_dim, h1_dim),          ## pre-layer size (h2) => (h1) post-layer size
                     optim_type=opt_type,             ## Optimizer
                     weight_init=w2_init,             ## W2[t0]
                     w_bound=w_bound,                 ## -1: deactivate the bouding
                     sign_value=-1.,                  ## Minimization
                     eta=eta,                         ## lr
)
W1 = BackwardSynapse("W1",
                     shape=(h1_dim, in_dim),          ## pre-layer size (h1) => (x) post-layer size
                     optim_type=opt_type,             ## Optimizer
                     weight_init=w1_init,             ## W1[t0]
                     w_bound=w_bound,                 ## -1: deactivate the bouding
                     sign_value=-1.,                  ## Minimization
                     eta=eta,                         ## lr
)
```







<!-- ----------------------------------------------------------------------------------------------------- -->

##### Wire Component:


The signal pathway is according to Rao & Ballard 1999.
Error is information goes from buttom to up in the forward pass.
Corrected prediction comes back from top to the down in the backward pass.


```python
            ######### feedback (Top-down) #########
            ### actual neural activation
            e2.target << z2.z
            e1.target << z1.z

            ### Top-down prediction
            e2.mu << W3.outputs
            e1.mu << W2.outputs
            e0.mu << W1.outputs

            ### Top-down prediction errors
            z1.j_td << e1.dtarget
            z2.j_td << e2.dtarget

            W3.inputs << z3.zF
            W2.inputs << z2.zF
            W1.inputs << z1.zF
```


```python
            ######### forward (Bottom-up) #########
            ## feedforward the errors via synapses
            E3.inputs << e2.dmu
            E2.inputs << e1.dmu
            E1.inputs << e0.dmu

            ## Bottom-up modulated errors
            z3.j << E3.outputs
            z2.j << E2.outputs
            z1.j << E1.outputs
```


```python
            ######## Hebbian learning #########
            ## Pre Synaptic Activation
            W3.pre << z3.zF
            W2.pre << z2.zF
            W1.pre << z1.zF

            ## Post Synaptic residual error
            W3.post << e2.dmu
            W2.post << e1.dmu
            W1.post << e0.dmu
```





```python
        ######### Process #########

        ## pin/tie feedback synapses to transpose of forward ones
        E1.weights.set(jnp.transpose(W1.weights.value))
        E2.weights.set(jnp.transpose(W2.weights.value))
        E3.weights.set(jnp.transpose(W3.weights.value))

        ## reset/set all components to their resting values / initial conditions
        circuit.reset()
        ########################################################################
        ## Perform several E-steps
        circuit.clamp_input(obs)
        circuit.process(jnp.array([[dt * i, dt] for i in range(T)]))

        ## Perform M-step (scheduled synaptic updates)
        circuit.evolve(t=T, dt=1.)
        ########################################################################
        ## Post-processing / probing desired model outputs
        obs_mu = e0.mu.value          ## get reconstructed signal
        L0 = e0.L.value               ## calculate reconstruction loss
```





<!-- ----------------------------------------------------------------------------------------------------- -->
<!-- ----------------------------------------------------------------------------------------------------- -->

#### Train PC model




<!-- -----------------------------------------------------------------------------------------------------
> **Some final words**
> As someone with background in computer science and computational math I personally found reading old papers as this one challenging when lack of required backgrounds. On the other hand growing with newer concepts in science and tech, some of the stuffs might look very obvious at first which brings confusing, and determining what has been established before and the predictive coding and what makes it so interesting seems unclear at first; at least to me. Here I decided to teach the predictive coding to me, who couldn't find the glory at first but got fascinated when they delve deeper. 
Here, I attempted to reflect my first principal in learning. I build understanding by fundamentals, only then I am allowed to acquire knowledge by reading recent advancements which is deepening the fundamentals into brain structure. The intuition for me is built via my curiousity to explore and analyze the collective behavior of individual components in neural network when grouped, throughout first 2 years of my PhD, on paper with my pen.
Here, I attempted to keep every piece original and every piece is made by my understanding of the field fundamentals. I hope you enjoy reading my tutorial and fascinate by the predictive coding.
-->
