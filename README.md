# logistic_growth
R scripts for a reproducible analysis of logistic growth
#Script to estimate the model parameters using a linear approximation

install.packages("dplyr")
library(dplyr)
#### The dplyr package enables us to manipulate data via efficient filtering, grouping and arranging. It will therefore be useful in managing this set of data.

growth_data <- read.csv("experiment1.csv")

# Case 1. K >> N0, t is small

data_subset1 <- growth_data %>% filter(t<1800) %>% mutate(N_log = log(N))

model1 <- lm(N_log ~ t, data_subset1)

summary(model1)

#### Initially, we are defining the linear model for the first part of the graph (where the growth is exponential), by filtering the data such that it only includes rows where t is less than 1800. Based on this data, the intercept is 6.903e+00, the gradient is 9.990e-03.

# Case 2. N(t) = K

data_subset2 <- growth_data %>% filter(t>1800)

model2 <- lm(N ~ 1, data_subset2)

summary(model2)

#### Here, we are defining the linear model according to values of t which exceed 1800, where growth is no longer exponential and begins to plateau
