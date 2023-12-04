# logistic_growth
R scripts for a reproducible analysis of logistic growth
#Script to estimate the model parameters using a linear approximation
```{r}
install.packages("dplyr")
library(dplyr)
```
The dplyr package enables us to manipulate data via efficient filtering, grouping and arranging. It will therefore be useful in managing this set of data.
```{r}
growth_data <- read.csv("experiment1.csv")
```
#### Firstly, we are reading in our data and calling it growth_data

# Case 1. K >> N0, t is small
```{r]
data_subset1 <- growth_data %>% filter(t<1800) %>% mutate(N_log = log(N))

model1 <- lm(N_log ~ t, data_subset1)

summary(model1)
```
We first want to determine estimates for the carrying capacity, initial population size and the population growth rate. We define a linear model for when t is small, and where we expect the growth to be exponential, by filtering the data such that it only includes rows where t is less than 1800 (beyond this point the growth is expected to plateau, based on the raw data). 

Then, we have mutated the population (N) to log transform it, because this results in 2 distinct growth stages - an initial increasing linear growth stage and a plateau whereby growth rate is constant - in order to create 2 separate linear models. We can consequently use these models to estimate growth rates, carrying capacity and population size as they will provide us with estimates of both the gradient and the y-intercept. For example, when t<1800, the intercept is 6.903e+00, the gradient is 9.990e-03.

# Case 2. N(t) = K
```{r}
data_subset2 <- growth_data %>% filter(t>1800)

model2 <- lm(N ~ 1, data_subset2)

summary(model2)
```
Next, we want to create a model for the stage of growth where we expect to observe a plateau, hence have filtered the data to only include values of t greater than 1800. 

We require 2 separate linear models because we predict there to be 2 distinct growth stages.


# Script to plot the logistic growth data
```{r}
growth_data <- read.csv("experiment1.csv")

install.packages("ggplot2")
library(ggplot2)

ggplot(aes(t,N), data = growth_data) +
  
  geom_point() +
  
  xlab("t") +
  
  ylab("N") +
  
  theme_bw()
```
This chunk of code plots a graph of the raw data, with time (t) on the x-axis and population size (N) on the y.

```{r}
ggplot(aes(t,N), data = growth_data) +
  
  geom_point() +
  
  xlab("t") +
  
  ylab("N ") +
  
  scale_y_continuous(trans='log10')
```
Here, we have plotted a graph of the raw data, except with a log transformation of the y-axis. 


# Script to plot data and model
Next, we will plot the model and compare it to the raw data in order to determine how accurately our model can predict variables of interest.
```
growth_data <- read.csv("experiment1.csv")

logistic_fun <- function(t) {
  
  N <- (N0*K*exp(r*t))/(K-N0+N0*exp(r*t))
  
  return(N)
  
}

N0 <- 6.903e+00 
  
r <- 9.990e-03
  
K <- 5.903e+10
```
After reading in the growth data, we define a function for logistic growth (logistic_fun) which will calculate values of N using the equation for logistic growth, as defined in the code.

```
ggplot(aes(t,N), data = growth_data) +
  
  geom_function(fun=logistic_fun, colour="red") +
  
  geom_point()+
  scale_y_continuous(trans='log10')
``` 
#Plotting the model to see how well it fits the data
