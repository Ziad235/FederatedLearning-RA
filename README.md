
# The Effects of Using Synthetic Data in a Federated Learning Enviornment 

## Background Information

This stage of research is a continuation of a "further experiemnts" step in [Professor Fida Dankar's](https://scholar.google.ae/citations?user=JvxSJRwAAAAJ&hl=en) previous [paper](https://ieeexplore.ieee.org/document/10068615). <br /> 
The results of this experiment are currently being typed up and will then be submitted for publication.

## Research Hypothesis 

Using synthetic data on any machine learning model in a Federated Learning enviornment results in a statistically significant decrease in the total number of iterations and computational time needed for global model convergence while still maintaining a comparable accuracy[^1] to the global model that was achieved without the use of synthetic data. 

[^1]: The differences between the final global model's performance when using synthetic data and not using synthetic data are statistically insignificant.

## Research Methods

### Enviornment Setup
To create a Federated Learning enviornment, I used [TensorFlow Federated API](https://www.tensorflow.org/federated/api_docs/python/tff).

### Machine Learning Model 
I used a logisitc regression model as the main machine learning model for each client, since linear regression was used in the original paper instead. <br />

### Synthetic Data Generator
To generate the synthetic data, I automated the process of using synthpop (non-parametric) synthetic data generator that can be found in this [repository](https://github.com/hazy/synthpop).

### Credibility of Final Global Model 
To have concrete criterea for global model convergence, I used Binary Cross Entropy and Categorical Cross Entropy (which are basically Logistic Loss functions for binary and categorical classification, rspectively). <br />

Within those loss (cost) functions, I incroporated elastic-net regularization in order to enhance model accuracy, and I used gradient descent to optimize the choice of model parameters with each client-server iteration. <br />

### Global Model Metrics 
To have concrete evidence that supports the hypothesis, I used a total of 5 metrics to compare final results.

1. <ins> Total Number of Iterations for Global Model Convergence </ins> <br />
This measure is a discrete value (_read: natural number_) that represents the total number of times for client-server iterations required to reach global model convergence 

2. <ins> Total (Computational) Time for Global Model Convergence </ins> <br />
This measure is a continuous value (_read: positive real number_) that represents the total time taken required to reach global model convergence.

3. <ins> Logistic Loss Function Value of Final Global Model </ins> <br />
This measure is a continuous value (_read: positive real number_) between 0 and 1 (inclusive), which represents the error margin/rate of the final global model. <br />
For elaboration, the closer the value is to 0 the less error in predicition.

4. <ins> Logarithmic Likelihood </ins> <br />
This measure is a continuous value (_read: non-positive real number) between $-\infty$ and 0 that represents how well the final globel model fits the overall data. <br />
For elaboration, the closer the value is to 0 the better fit the model is to the overall data.

5. <ins> Crude Approximate Accuracy </ins> <br />
This measure is a continuous value (_read: positive real number_) between 0 and 1 that represents an approximation of model prediciton accuracy (the closer to 1 the more accurate). <br />
For context, this metric is given by simply evaluating $e^{-LL}$, where $LL$ is the Logistic Loss value of the final global model.

## Data
I used 6 distinct datasets (retrieved from UCI except one of them, which was personally sent to me by Professor Fida), each with its own number of clients. <br />
The datasets had outcome variables that were either binary or categorical. <br />
Further information about the datasets can be found in the __Project_Information__ folder.

## Results
The results confirmed our hypothesis, with a substantial differences in total number of iterations and computational time needed for global model convergence and comparable accuracies. <br />
Further details can be found in the __Project_Information__ folder.

## Further Notes
Please read the __Project_Information__ folder to learn and understand more about this project and its impactful results. <br />

Federated Learning is a ground-breaking idea that advances the use of data privacy in and brings it at the forefront of producing highly scalable and reliable models. <br />

Feel free to reach out to [me](mailto:zmh6339@nyu.edu) and/or [Professor Fida Dankar](mailto:fd2242@nyu.edu) for any questions. <br />

*_Please note that for (intellectual) copyright reasons, concrete code regarding main content of this project cannot be published now until the typed up paper is submitted and accepted for publishing._*

