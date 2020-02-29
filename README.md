# QAOA Weight Maxcut

## Discussion of Results
Based on the output by the QAOA algorithm, the most frequent bitstring is 1101. The bitstring, if read backwards, corresponds to the nodes in the graph such that the 0 measured from the first qubit is the 4rth node on the graph. 

The MaxCut problem seeks to colour the nodes of a graph (with 2 different colours) such that the number of nodes coloured the same that are directly connected to each other by edges is minimized (aka the maximum number of cuts possible). 

The 0 and 1 can be interpreted as either colour: if we take 0 as pink and 1 as blue , the resulting MaxCut on the graph inputted into the QAOA algorithm will look like this:

<img src="https://github.com/lanabozanic/QAOA_Weight_Maxcut/blob/master/maxcut.PNG" alt="MaxCut Result" width="250">

## The QAOA Algorithm
The Quantum Approximate Optimization Algorithm doesn't actually solve for the exact max value, but instead approximates it (hence the creative name). Although there are many classical algorithms that can do this already, QAOA has the potential to show speed ups over the classical algorithms as the circuit depth, p -> ∞ . At this point in time, the best performance we've achieved with the QAOA algorithm is at depth p = 1, so there is still much more exploring to do. The goal of QAOA is to optimize for some value, z, that maximizes the cost function, $C = \displaystyle \sum_{k=1}^{m} C_m(z)$, where $ z = z_1z_1...z_k$. But since we're not actually aiming for the exact value, just a really good approximation, our goal is to find a  $ \dfrac{C(z)}{C_{max}} $ such that their ratio gets closer and closer to 1   (i.e. $ C(z) $ gets closer and closer to $ C_{max} $)

### Quantum-ness

The maximum value of $C(z')$ can be represented by the expectation value, $ \langle z' |C| z' \rangle $. What QAOA does is it applied a series of rotations of $e^{-i\gamma H_C}$ a$e^{-i\beta H_B}$. 

$H_C$ represents the problem hamiltonian, where $H_C = C(\sigma^{z}_{1}, \sigma^{z}_{2},...,\sigma^{z}_{N})$, which we mapped from our cost function. Each variable of $z_k$ is represented with a quantum spin of $\sigma^{z}_{i}$

$H_B$ represents the mixing Hamiltonian, where $H_B$ = $\displaystyle \sum_{j=1}^{N} \sigma^{x}_{j}$

By iterating through a series of these rotations on a given state, $ | \psi \rangle $ the expectation value of $\langle \psi(\gamma,\beta) |C| \psi(\gamma,\beta) \rangle $ gets closer and closer to the max expectation value of $\langle z|C|z \rangle$.

### Classical-ness 

Now that we have all the quantum-ness sorted out, we introduce the classical part of this hybrid algorithm. The classical part is used for measurement and optimization of parameters. With each iteration, we send through new optimized parameters, $\gamma$ and $\beta$, so that each time we evalute the original cost function we get a greater value.

### Step-by-Step guide
1. **Start with a trial state $|\psi \rangle$**   
2. **Initialize 2 params, $\gamma$ and $\beta$**: You can base the initial params off a good ansatz, other wise they will start at 0.
3. **Construct new state $|\psi(\gamma,\beta)\rangle$:** --> |$\psi\rangle$ gets updated.
4. **Measure |$\psi(\gamma,\beta)\rangle$** classically 
5. **Iterate through steps 1-4^^:** $\langle\psi(\gamma,\beta)\rangle$ will get closer to the optimal $|z\rangle$ with each iteration
6. **Calculate expectation value** $\langle\psi(\gamma,\beta)|C|\psi(\gamma,\beta)\rangle$ classically which will gets closer in closer to $\langle z|C|z\rangle$ (which is our max. cost)
7. **Reiterate** with new parameters (steps 3 - 6): Take the highest average cost, and that's your maximized function value!

