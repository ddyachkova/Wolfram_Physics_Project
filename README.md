### Motivation, Goal and Background
The notion of dimension is crucial for characterizing the limiting behaviors of the models, especially when the traditional geometrical structures of the graphs 
  are not readily recognizable. The progression of dimensionality with an increased number of steps can tell us two things about a universe that is being studied. First, 
  whether it is static, contracting, or expanding. And second, we get a better idea about the behavior of the universe at its boundary effects. 
	  Usually, to approximate the dimensionality of the graph, we look at the Hausdorff dimension and calculate the log difference between the neighborhood hypervolume 
  values. Essentially, we approximate d in the scaling law `V = r^d`, where V is the volume of a graph, and r is the distance from the central node to its 
  neighbors. The question is, what happens to the volume when d is a function of time, i.e., the number of evolutions. A solution proposed in this project is to use the
  values the the neighborhood volume to fit a linear regression, record the slope, and classify the rules based on those results. The slope is then in units of dimensions. 	 
    However, we also find that this type of dimensionality approximation is not efficient. First, it is sensitive to boundary effects, and thus can be not 
  representative of the true dimensionality of the universe in that part of the range. We propose an alternative approach using the spectral dimension. 
  We find an average length of a random walk starting from the most connected node, and use those values to learn about the correlation with the number of evolutions. We have 
  to set some constraints onto the signatures and the states of the graph. The project is only implemented for `2_2 -> 3_2` signatures and only for connected 
  hypergraphs. The caveat of the disconnected case is in the definition of dimension - one would need to decide whether only to consider the largest connected component or 
  something alternative.
  
  ### Variable
There are three variables that we can vary:
-  the initial conditions of the hypergraphs based on the signature; 
-  the update  rules based on the signature; 
-  the way that the rules are applied, i.e. least recent edge/random. 

Here,we only work with the first two, i.e.explore the variation with the initial conditions as well as the variation with different rules. 

Let's begin with a demonstration of the approach on the classic example.

### Example 
Let' s consider a simple grid corresponding to a `2_2 -> 3_3` rule. 

``` eo = WolframModel[{{1, 2, 2}, {3, 1, 4}} -> {{2, 5, 2}, {2, 3, 5}, {4, 5, 5}}, {{0, 0, 0}, {0, 0, 0}}, 200]; eo["FinalStatePlot"] ```


<img src="https://github.com/ddyachkova/Wolfram_Physics_Project/blob/master/Graphics/graph1.jpg" width="40%" height="40%">


### Hausdorff dimension
Now, let' s have a look at a Hausdorff dimension approximation. 

<img src="https://github.com/ddyachkova/Wolfram_Physics_Project/blob/master/Graphics/graph2.jpg" width="40%" height="40%">

The code below fits the linear regression to the curve and outputs the slope. 
``` 
rma = ResourceFunction["RaggedMeanAround"][Values[ResourceFunction["HypergraphNeighborhoodVolumes"][eo["FinalState"]]]];
p=Predict[Range[Length[rma]]-> rma,Method->"LinearRegression"];
pred = p[Range[Length[rma]]];
slope = (pred[[-1]] - pred[[1]])/Length[pred];
gr = List[rma, pred]; Show[ListLinePlot[Table[gr[[i]], {i, 1, Length[gr]}]]]
``` 

<img src="https://github.com/ddyachkova/Wolfram_Physics_Project/blob/master/Graphics/graph3.jpg" width="40%" height="40%">

### Spectral dimension

Below is the code for the spectral dimension approximation. We run a random walk using thee adjacency matrix as a set of the update rules.  Essentially, it is a 
Markov chain with a uniform probability distribution for each node that is connected to the starting node. Here is the result of the spectral dimension approximation 
for the example graph. 

<img src="https://github.com/ddyachkova/Wolfram_Physics_Project/blob/master/Graphics/dims.png" width="40%" height="40%">

### Results

For the chosen signature, we have eight initial conditions. 

<img src="https://github.com/ddyachkova/Wolfram_Physics_Project/blob/master/Graphics/init_cond.png" width="80%" height="80%">

The histograms above show the distribution of the slope values for the initial condition values. We selected all of the rules that lead to connected hypergraphs. 
As we can see, the majority of the the rules have dimensionality curves with zero slopes, which indicate stable universes. 

<img src="https://github.com/ddyachkova/Wolfram_Physics_Project/blob/master/Graphics/hists.png" width="80%" height="80%">

For the spectral dimension the results are the following. There are much less samples in this case due to computational complexity. We can see that for some conditions, we are getting negative slopes. That is an indicator of contracting universes. 

<img src="https://github.com/ddyachkova/Wolfram_Physics_Project/blob/master/Graphics/hists2.png" width="80%" height="80%">


### Conclusions
We can conclude two things. First, we got a proof that there are stable, contracting and expanding universes. And the number of stable universes with the chosen signature `2_2 -> 3_2` is prevalent. Second, dimensionality approximation with neighborhood volume is not effective during the sensitivity to the boundary conditions. An alternative approach with spectral dimension that uses averaged random walks for each evolutionary state is more representative, however also computationally expensive. 
The insights we got about the universes are relevant to the study of the early inflation models. 

### Acknowledgments 
A huge thanks to Jack Heimrath and Jonathan Gorard, who were wonderful and supportive mentors throughout the project. Also to Kiel Howe - a professor at Minerva Schools who provided theoretical and practical preparation for the physics track. Additionally, I thank Stephen Wolfram and the Summer School organizers for a remarkable opportunity to participate in this project. 
