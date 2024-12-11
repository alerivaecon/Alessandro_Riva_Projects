# **A simple Cake-Eating problem**
The following code provides the solution to a simple Cake-Eating problem I developed out of interest after I learned about the 
basics of Dynamic Programming in my Mathematical Economics class. Although simple, this code is able to highlight the main characteristics of Dynamic Programming, being a useful exercise to unite theoretical modeling with coding. 

In a Cake-Eating setting, an agent has to consume a finite amount of resource (the "cake") in 
a discrete horizon in order to maximize their total discounted utility. 

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

# **Solution**
The code solves this problem by backward induction in three steps.

First, vectors of  optimal consumption and the related utility in time periods $$t$$ and $$t - 1$$ are initialized.

Then, the code loops through all possible states of V associated with different consumption levels, selecting the one which gives maximal utility. 

Finally, the code provides a simulation that checks if the optimal consumption path is indeed the one proposed in the theoretical solution.


# **Code**

```python
import numpy as np

def solve_backwards(beta,W,T):
    # 1. Initialize
    Vstar_bi = np.nan+np.zeros([W+1,T])
    Cstar_bi = np.nan + np.zeros([W+1,T])
    Cstar_bi[:,T-1] = np.arange(W+1) 
    Vstar_bi[:,T-1] = np.sqrt(Cstar_bi[:,T-1])
    # 2. solve
    
    # Loop over periods
    for t in reversed(range(0,T-1,1)):  # backwards  
    
        # loop over states
        for w in range(W+1):
            c = np.arange(w+1)
            w_t_1 = w - c
            V_next = Vstar_bi[w_t_1,t+1]
            guess_V = np.sqrt(c)+beta*V_next
            Vstar_bi[w,t] = np.amax(guess_V)
            Cstar_bi[w,t] = np.argmax(guess_V)

    return Cstar_bi, Vstar_bi

beta = 0.9
W = 5
T = 3
C,V = solve_backwards(beta=beta, W=W, T=T)
print(C)

# 3. simulate
C_back = np.empty(T)
W_nw = W
for t in range(T):
    W_nw = int(W_nw)  
    C_back[t] = C[W_nw,t]  
    W_nw = W_nw-C_back[t]
display(C_back)
display(W_nw)



