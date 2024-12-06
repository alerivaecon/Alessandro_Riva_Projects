# **A simple Cake-Eating problem**
The following code provides the solution to a simple Cake-Eating problem I developed out of interest after I learned about the 
basics of Dynamic Programming in my Mathematical Economics class. 

In a Cake-Eating setting, an agent has to consume a finite amount of resource (the "cake") in 
a discrete time setting in order to maximize their total discounted utility. 

# **Setup of the problem**
In this specific problem, an agent has to consume a cake of size $W=5$ in $T=3$ periods,
with a discount factor of $\beta=0.9$. 

He derives utility from consumption according to the following Bellman equation:

$$
V_t^*(W_t) = \max_{0 \leq c_t \leq W_t} \left( \sqrt{c_t} + \beta V_{t+1}(W_{t+1}) \right)
$$
subject to:
$$
W_{t+1} = W_t - c_t, \quad c_t \in \mathbb{N}_0 \forall t.
$$

# **Code**

The code solves this problem by backward induction in three steps. 

First, vectors of optimal consumption $c_t^*$ and the related utility $V_t^*$ in time periods t
and $t-1$ are initialized. 

Then, the code loops through all possible states of V associated to different consumption levels,
selecting the one which gives maximal utility, thus being able to recover $V^*$ and $c^*$

Finally, the code 




