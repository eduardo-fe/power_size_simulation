# power_size_simulation
Code supporting LinkedIn post to show effect of increased sample size on Type I error and power. 

library(ggplot2)
set.seed(123)

simulate_test <- function(n, effect=0, alpha=0.05, reps=50000) {
  rejections <- replicate(reps, {
    x <- rnorm(n, mean = effect, sd = 1)  # one-sample t-test
    t.test(x, mu = 0)$p.value < alpha
  })
  mean(rejections)
}

sample_sizes <- c(50, 100, 500, 1000, 10000 )

# Run simulations
null_results <- sapply(sample_sizes, simulate_test, effect=0)
effect_results <- sapply(sample_sizes, simulate_test, effect=0.1)

# Prepare data for plotting
df <- data.frame(
  n = rep(sample_sizes, 2),
  rejection_prob = c(null_results, effect_results),
  scenario = rep(c("Null true (Type I error)", "Small effect (Power)"), each=length(sample_sizes))
)

# Plot
ggplot(df, aes(x = n, y = rejection_prob, color = scenario)) +
  geom_line() +
  geom_point() +
  geom_text(aes(label = round(rejection_prob, 3)), 
            vjust = -0.5, size = 3) +  # add labels above points
  geom_hline(yintercept = 0.05, linetype = "dashed", color = "black") + # nominal 5% line
  scale_x_log10() +  # log scale for clarity
  ylim(0,1) +
  labs(
    x = "Sample size (log scale)",
    y = "Probability of rejecting H0",
    title = "Effect of sample size on hypothesis test rejection",
    color = "Scenario"
  ) +
  theme_minimal()
