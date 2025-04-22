# Bayesian Analysis of Global Temperature Trends using MCMC

## Description

This project explores the trend in global temperature anomalies using Bayesian inference. I implemented a simple Bayesian linear regression model and estimated its parameters using a custom-built Metropolis-Hastings Markov Chain Monte Carlo (MCMC) algorithm in Python. The analysis is performed on publicly available global temperature data from NASA GISS.

The primary goal was to apply Bayesian techniques and MCMC sampling to a real-world environmental dataset, demonstrating the process of model definition, prior specification, MCMC implementation, convergence diagnostics, and posterior analysis.

## Dataset

* **Source:** NASA Goddard Institute for Space Studies (GISS) Surface Temperature Analysis (GISTEMP v4).
* **Data:** Global Land-Ocean Temperature Index (LOTI). This represents the deviation of global annual mean surface temperatures from the 1951-1980 baseline average, measured in degrees Celsius.
* **File Used:** `GLB.Ts+dSST.csv`
* **Download:** You can obtain the specific CSV file directly from NASA GISS:
    [https://data.giss.nasa.gov/gistemp/graphs_v4/graph_data/GLB.Ts+dSST/GLB.Ts+dSST.csv](https://data.giss.nasa.gov/gistemp/graphs_v4/graph_data/GLB.Ts+dSST/GLB.Ts+dSST.csv)
* **Requirement:** For the notebook (`*.ipynb`) to run correctly, please download this file and place it in the root directory of this repository. The notebook expects to find `GLB.Ts+dSST.csv` in the same folder.

## Model

I modeled the annual temperature anomaly ($T_a$) as a linear function of the year ($y$), assuming normally distributed errors ($\epsilon$):

$T_a(y) = \alpha + \beta \times (y - \bar{y}) + \epsilon$

where $\epsilon \sim N(0, \sigma^2)$.

The year variable ($y$) was centered by subtracting the mean year ($\bar{y}$) of the dataset to improve MCMC sampling efficiency.

The parameters estimated via MCMC are:
* $\alpha$: The intercept, representing the average temperature anomaly at the mean year.
* $\beta$: The slope, representing the average rate of change in temperature anomaly per year (°C/year).
* $\sigma$: The standard deviation of the model residuals.

## Methodology

* **Bayesian Inference:** Used a Bayesian approach to obtain posterior probability distributions for the model parameters, reflecting uncertainty.
* **Priors:** Weakly informative priors were chosen:
    * $\alpha \sim N(0, 10^2)$
    * $\beta \sim N(0, 1^2)$
    * $\sigma \sim \text{HalfCauchy}(1)$
* **MCMC Algorithm:** Implemented the Metropolis-Hastings algorithm from scratch to draw samples from the joint posterior distribution of ($\alpha, \beta, \sigma$).
* **Diagnostics:** Assessed MCMC convergence and mixing using trace plots and autocorrelation plots.

## Requirements

The analysis was performed using Python 3. The main libraries required are:

* `numpy`
* `pandas`
* `scipy`
* `matplotlib`
* `seaborn`
* `statsmodels` (specifically for `plot_acf`)

You can typically install these using pip:
`pip install numpy pandas scipy matplotlib seaborn statsmodels`



## Usage

1.  Ensure you have Python 3 and the required libraries installed.
2.  Download the dataset `GLB.Ts+dSST.csv` from the link provided above and place it in the root directory of this repository.
3.  Open the Jupyter Notebook file (e.g., `Bayesian_Linear_Regression_Temperature_MCMC.ipynb`) in a Jupyter environment (like Jupyter Lab, Jupyter Notebook, VS Code with Jupyter extension, or Google Colab).
4.  Run the notebook cells sequentially.

## Results

The MCMC simulation successfully generated samples from the posterior distributions of the model parameters. Key results visible in the notebook include:

* Trace plots indicating good mixing of the MCMC chains.
* Autocorrelation plots showing relatively quick decorrelation of samples.
* Posterior distributions for the intercept ($\alpha$), slope ($\beta$), and standard deviation ($\sigma$). The posterior for $\beta$ clearly indicates a positive warming trend.
* A visualization of the observed data overlaid with the posterior mean trend line and uncertainty bounds derived from posterior samples.

Please see the Jupyter Notebook for detailed code, visualizations, and analysis.

## License

This project is licensed under the [MIT License](LICENSE). *(Note: Make sure you actually add a file named `LICENSE` containing the MIT License text if you choose this)*
