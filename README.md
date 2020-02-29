# QAOA Weighted Maxcut

## Discussion of Results
Based on the output by the QAOA algorithm, the most frequent bitstring is 1101. The bitstring, if read backwards, corresponds to the nodes in the graph such that the 0 measured from the first qubit is the 4rth node on the graph. 

The MaxCut problem seeks to colour the nodes of a graph (with 2 different colours) such that the number of nodes coloured the same that are directly connected to each other by edges is minimized (aka the maximum number of cuts possible). 

The 0 and 1 can be interpreted as either colour: if we take 0 as pink and 1 as blue , the resulting MaxCut on the graph inputted into the QAOA algorithm will look like this:

<img src="https://github.com/lanabozanic/QAOA_Weighted_Maxcut/blob/master/maxcut-graph.PNG" alt="MaxCut Result" width="250">

## The QAOA Algorithm
Quick explanation on how the beta and gamma parameters are optimized to find our desired expecation value, corresponding to the MaxCut of the graph <a href='https://github.com/lanabozanic/QAOA_Weighted_Maxcut/blob/master/The_QAOA_Algorithm.ipynb'>here</a>

