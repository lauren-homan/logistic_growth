# Plotting the logistic against the exponential

Firstly, we must define the logistic and exponential functions;

```{r}
exponential_fun <- function(t) {
  N <- N0*exp(r*t)
  return(N)
}
  

logistic_fun <- function(t) {
  N <- (N0*K*exp(r*t))/(K-N0+N0*exp(r*t))
  return(N)
}
```
These can now be used to plot both functions on the same plot;

```{r}
ggplot(data.frame(t = seq(0, 4000)), aes(t)) +
  geom_line(aes(y = logistic_fun(t)), colour = "red") +
  geom_line(aes(y = exponential_fun(t)), colour = "blue") +
  scale_y_continuous(trans = 'log10') +
  labs(title = "Exponential vs Logistic Function",
       x = "t",
       y = "N")
```

Here, I have created a dataframe for the values of t ranging from 0-4000. This enables both the logistic and exponential functions to be plotted between the times 0-4000, but means the raw data itself is not included. 

       
