# Quantum Chemistry
First off, you're probably wondering what I mean by "quantum chemistry." Fear not, I will not be discussing quantum mechanics in any depth. Quantum chemistry, as I'll be using the term, refers to the electronic (as in electrons) properties of molecules, as calculated at different levels (differing in either approximation methods or assumptions made) of quantum theory. This project is meant to predict chemical properties using machine learning methods, which are orders of magnitude faster than the explicit quantum mechanical solutions.
<br><br>
For example, one property predicted is the atomization energy of the molecule. This is relatively simple: the amount of energy required to break apart (dissociate) a molecule into its component atoms. Another property is the absorption frequency, the frequency of light that the molecule absorbs best (the molecule absorbs a higher proportion of this frequency than any other frequency).

## Dataset
This project uses the [QM7b](http://quantum-machine.org/data/qm7b.mat) dataset, consisting of about 7000 small (<= 24 atoms) organic molecules. The features are the elements of each molecule's Coulomb Matrix: a 2-dimensional array that encodes each atom's atomic charge (number of protons/electrons) and its Cartesian (XYZ) coordinates. For each molecule there are 9 unique properties, some of which have values given for multiple levels of quantum theory, for a total of 14 predicted properties.

## Model
All 14 properties are modeled with a single deep neural network, set up for multi-task learning, meaning that the output layer has one node for each property. This has a few advantages: you can use a single model for all properties, and training to predict one property will also provide some training for any correlated properties, making use of the shared information in the hidden layers. Hyperparameter search was performed in a validation loop using [Bayesian Optimization](https://github.com/fmfn/BayesianOptimization), an extension of randomized search that uses information from previous trials to find areas which are likely to have good outcomes. Try it, it's miles better than grid search, if a little tricky to set up.

## Built With
[Amazon Web Services](https://aws.amazon.com) - GPU training
<br>
[BayesianOptimization](https://github.com/fmfn/BayesianOptimization) - A Python implementation of global optimization with gaussian processes.

## Citations
Montavon, Grégoire, et al. "Machine learning of molecular electronic properties in chemical compound space." New Journal of Physics 15.9 (2013): 095003.

[Presentation slides here.](https://docs.google.com/presentation/d/1p5l8TwGy8yM_qyIMAROS_xQFoyJM3QBVHRz9r4O4c_o/edit?usp=sharing)
