#Tree Based Methods

* Basically stratifying or segmenting the predictor space into a number of simple regions. In order to make a prediction for a given observation, we typically use the mean or the mode of the training observations in the region to which it belongs.

* Since the set of splitting rules used
to segment the predictor space can be summarized in a tree, these types of
approaches are known as decision tree methods.

### Constructing the regions
* The goal is to find boxes R1, . . . , RJ that minimize the RSS,
given by 
<math>\begin{equation}
\sum_{j=1}^{J} \sum_{i \in R_{j}}\left(y_{i}-\hat{y}_{R_{j}}\right)^{2}
\end{equation}</math>

where ˆyRj is the mean response for the training observations within the
jth box.

* Top Down, Greedy aproach [Recursive Binary Splitting] : 
	* The recursive binary splittin approach is top-down because it begins at the top of the tree (at which point all observations belong to a single region) and then successively splits the predictor space; each split is indicated via two new branches further down on the tree.
	* It is greedy because at each step of the tree-building process, the best split is made at that particular step, rather than looking ahead and picking a split that will lead to a better tree in some future step.
* At every split we try to find the predictor and the exact split value which reduces the RSS

### Tree Pruning
* The tree may grow deep overfitting the train data.
* A smaller tree with fewer regions might be a better model
* One way - stop the splitting if decrease in RSS exceeds some threshold-short-sighted - not always good because one bad split earlier might lead to a good split in the later stages.
* Grow a large tree and prune it to the best subtree - in terms of RSS - evaluated by cross-valdiation. Doing this for every possible subtree is cumbursome
* Cost complexity pruning - Weakest link pruning - Similar to Lasso 


### Classification tree
* we predict that each observation belongs to the most commonly occurring class of training
observations in the region to which it belongs
* natural alternative to RSS is the classification error rate
* Gini Index- a measure of node purity - <math>\begin{equation}
G=\sum_{k=1}^{K} \hat{p}_{m k}\left(1-\hat{p}_{m k}\right)
\end{equation}</math>


* 



