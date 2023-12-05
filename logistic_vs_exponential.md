# Plotting the logistic against the exponential

```{r}
ggplot(data.frame(t = seq(0, 4000)), aes(t)) +
  geom_line(aes(y = logistic_fun(t)), colour = "red") +
  geom_line(aes(y = exponential_fun(t)), colour = "blue") +
  scale_y_continuous(trans = 'log10') +
  labs(title = "Exponential vs Logistic Function",
       x = "t",
       y = "N")
```

Here, we have created a 

       
