# 1. Simulating a random walk
```{r}
#install.packages("ggplot2")
#install.packages("gridExtra")

library(ggplot2)
library(gridExtra)

random_walk  <- function (n_steps) {
  
  df <- data.frame(x = rep(NA, n_steps), y = rep(NA, n_steps), time = 1:n_steps)
  
  df[1,] <- c(0,0,1)
  
  for (i in 2:n_steps) {
    
    h <- 0.25
    
    angle <- runif(1, min = 0, max = 2*pi)
    
    df[i,1] <- df[i-1,1] + cos(angle)*h
    
    df[i,2] <- df[i-1,2] + sin(angle)*h
    
    df[i,3] <- i
    
  }
  
  return(df)
  
}
```
A dataframe is created containing 3 variables: x, y and time. The code simulates a 'random walk' according to x- and y-coordinates, meaning the 

```{r}
data1 <- random_walk(500)

plot1 <- ggplot(aes(x = x, y = y), data = data1) +
  
  geom_path(aes(colour = time)) +
  
  theme_bw() +
  
  xlab("x-coordinate") +
  
  ylab("y-coordinate")
```

```{r}

data2 <- random_walk(500)

plot2 <- ggplot(aes(x = x, y = y), data = data2) +
  
  geom_path(aes(colour = time)) +
  
  theme_bw() +
  
  xlab("x-coordinate") +
  
  ylab("y-coordinate")

grid.arrange(plot1, plot2, ncol=2)
```

Here, 2 different 'random walk' graphs have been plotted using the ggplot2 function, each with 500 steps. Despite the fact that both plots use the same code and plot 500 steps, due to the randomness of the walks the graphs appear completely different in terms of the patterns of x- and y-coordinates with respect to time. Similarly, when the code is re-run, the plots appear differently, because of the fact that the direction taken is random. This is because direction is random with respect to time. 
Time is demonstrated here by use of a colour key - the darker the shade of blue the more time has been spent walking.


# 2. Random seeds

A random seed is a method used in R for generating a pseudorandom number. It is an integer vector generated with an algorithm, but requires a 'seed' to initialise. Hence, the number produced is pseudorandom because if you know both the seed and the generator, you can predict and reproduce the outcome. The algorithm random number generator (RNG) mimics the properties of the independent generation of numbers within a distribution in the interval (0,1).
(information was sourced from r-coder.com)
