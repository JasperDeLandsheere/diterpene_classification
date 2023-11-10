# diterpene_classification
For my Theoretical Foundations of Machine Learning course, I was presented with the following task:
*In NMR experiments, molecules are placed in a strong magnetic field, resulting in the molecules resonating at a specific frequency. These frequencies can then be used to infer information about the molecules' chemical structures. The given dataset comprises of 1503 spectra of diterpenes, classified into 23 different classes according to their skeleton structure. The goal is to predict the class of a given spectrum.* 

For a more detailed description of the classification task and the data, please refer to the original paper by Dzeroski et al. (I have included the paper in the repository).

The task seems straight forward at first, but as my team and I noticed quickly, there is a **catch**. In this repository, I will show a possible solution that I implemented and got a pretty good result.

## The catch: does order matter?
The data is described by:
- expert designed features (we ignore these),
- an ID
- a number of resonance frequencies with their "multiplicity"
- a class label

Usually, in machine learning, we work with $x \in \mathbb{R}^k$, with $k$ many features, and:  
- **order does matter**: $i$ th attribute $x_i$ of $x$ corresponds to $x_i'$ of $x'$

On this dataset, the order of the multiplicity-frequency pairs $(m, f)$ does not matter!  
$m ∈ \{s, d,t, q\}$ and $f ≥ 0$  
So, the algorithm $f(x)$ has to be **order-independent**, i.e., **permutation-invariant**:  
- $x = ((d, 53), (d, 52), (q, 72))$ and
- $x = ((q, 72), (d, 52), (d, 53))$
- should be treated exactly the same: $f(x) = f (x')$

Basically, we should treat $x$ as a set and not as a sequence.

## (my) Solution
To solve this, I used a permutation-invariant kernel (I used the RBF kernel). Specifically, you can compare all pairs of frequencies with the same multiplicity and then sum them up. Then, I just used a SVM. See code for more details! Note: this is not the full assignment, just a part I worked on. It includes testing some code and no full documentation.