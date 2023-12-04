# logistic_growth
R scripts for a reproducible analysis of logistic growth
#Script to estimate the model parameters using a linear approximation
```{r}
install.packages("dplyr")
library(dplyr)
```
#### The dplyr package enables us to manipulate data via efficient filtering, grouping and arranging. It will therefore be useful in managing this set of data.
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
#### Initially, we are defining the linear model for the first part of the graph (where the growth is exponential), by filtering the data such that it only includes rows where t is less than 1800. Here, we have log transformed the population size (N) data, because this results in 2 distinct growth stages - an initial linear growth and then a plateau. We can consequently use this model to determine initial growth rates, as it will provide us with estimates of both the gradient and the y-intercept. Based on this data, the intercept is 6.903e+00, the gradient is 9.990e-03.

# Case 2. N(t) = K
```{r}
data_subset2 <- growth_data %>% filter(t>1800)

model2 <- lm(N ~ 1, data_subset2)

summary(model2)
```
#### Here, we are defining the linear model according to values of t which exceed 1800, at which point growth is no longer exponential and begins to plateau. We filter the data initially 


# Script to plot the logistic growth data
```{r}
growth_data <- read.csv("experiment1.csv")

install.packages("ggplot2")
library(ggplot2)

ggplot(aes(t,N), data = growth_data) +
  
  geom_point() +
  
  xlab("t") +
  
  ylab("y") +
  
  theme_bw()
```
#### This chunk of code plots a graph of our raw data, without a log-transformation on the y-axis. 

ggplot(aes(t,N), data = growth_data) +
  
  geom_point() +
  
  xlab("t") +
  
  ylab("y") +
  
  scale_y_continuous(trans='log10')
