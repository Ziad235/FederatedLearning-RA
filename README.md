
# The Effects of Using Synthetic Data in a Federated Learning Enviornment 

>## Background Information
This stage of research is a continuation of a "further experiemnts" step in [Professor Fida Dankar's](https://scholar.google.ae/citations?user=JvxSJRwAAAAJ&hl=en) previous [paper](https://ieeexplore.ieee.org/document/10068615). <br /> 
The results of this experiment are currently being typed up and will then be submitted for publication.
---
>## Research Hypothesis 
Using synthetic data on any machine learning model in a Federated Learning enviornment results in a statistically significant decrease in the total number of iterations and computational time needed for global model convergence while still maintaining a comparable accuracy[^1] to the global model that was achieved without the use of synthetic data. 
---
[^1]: The differences between the final global model's prediction accuracy, model fit, and error rate when using synthetic data and not using synthetic data are statistically significant.

>## Research Methods

+ ### Enviornment Setup
To create a Federated Learning enviornment, I used [TensorFlow Federated API](https://www.tensorflow.org/federated/api_docs/python/tff).

+ ### Machine Learning Model
I used a logisitc regression model as the main machine learning model for each client, since linear regression was used in the original paper instead. <br />

+ ### Synthetic Data Generator
To generate the synthetic data, I automated the process of using synthpop (non-parametric) synthetic data generator that can be found in this [repository](https://github.com/hazy/synthpop).

+ ### Credibility of Final Global Model
To have concrete criterea for global model convergence, I used Binary Cross Entropy and Categorical Cross Entropy (which are basically Logistic Loss functions for binary and categorical classification, rspectively). <br />

Within those loss (cost) functions, I incroporated elastic-net regularization in order to enhance model accuracy, and I used gradient descent to optimize the choice of model parameters with each client-server iteration. <br />

+ ### Global Model Metrics
To have concrete evidence that supports the hypothesis, I used a total of 5 metrics to compare final results.

1. <u> Total Number of Iterations for Global Model Convergence </u>
This measure is a discrete value (_read: natural number_) that represents the total number of times for client-server iterations required to reach global model convergence 

2. <u> Total (Computational) Time for Global Model Convergence </u>
This measure is a continuous value (_read: positive real number_) that represents the total time taken required to reach global model convergence.

3. <u> Logistic Loss Function Value of Final Global Model </u>
This measure is a continuous value (_read: positive real number_) between 0 and 1 (inclusive), which represents the error margin/rate of the final global model. <br />
For elaboration, the closer the value is to 0 the less error in predicition.

4. <u> Logarithmic Likelihood </u>
This measure is a continuous value (_read: non-positive real number) between $-\infty$ and 0 that represents how well the final globel model fits the overall data. <br />
For elaboration, the closer the value is to 0 the better fit the model is to the overall data.

5. <u> Crude Approximate Accuracy </u>
This measure is a continuous value (_read: positive real number_) between 0 and 1 that represents an approximation of model prediciton accuracy (the closer to 1 the more accurate). <br />
For context, this metric is given by simply evaluating $e^{-LL}$, where $LL$ is the Logistic Loss value of the final global model.

