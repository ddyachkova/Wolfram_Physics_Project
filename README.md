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

