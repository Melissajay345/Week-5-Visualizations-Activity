---
title: "Visualization Activity"
author: "Melissa Jayawardane"
output: word_document
date: "2023-06-19"
---

```{r setup, include=FALSE, message=FALSE, warning=FALSE}
knitr::opts_chunk$set(echo = TRUE)
```

## Data Visualization
```{r}
# Read the dataset into R using read.csv() function
df<-read.csv("C:/Users/user/Documents/ds_salaries.csv") 
str(df)
```
```{r}
library(ggplot2)
# Calculate the range of the data
data_range <- max(df$salary) - min(df$salary)

# Estimate the bin width using the Freedman-Diaconis rule
bin_width <- 2 * IQR(df$salary) / (length(df$salary)^(1/3))

# Calculate the number of groups
num_groups <- ceiling(data_range / bin_width)

# Create a histogram with the estimated number of groups
ggplot(df, aes(x = salary)) +
  geom_histogram(binwidth = bin_width, fill = "skyblue", color = "black") +
  labs(title = "Salary Distribution",
       x = "Salary",
       y = "Frequency") +
  scale_x_continuous(breaks = seq(min(df$salary), max(df$salary), by = bin_width))

```

The above histogram represents the salary distribution across the market. It is evident from the plot that the distribution is skewed to the left, with majority of the employees in the industry having lower-end salaries.
```{r}
# Create a bar plot of company size distribution
ggplot(df, aes(x = company_size)) +
  geom_bar(fill = "skyblue", color = "black") +
  labs(title = "Company Size Distribution",
       x = "Company Size",
       y = "Count")

```

Based on the above plot, most of the companies are medium size. If the majority of companies in the dataset are categorized as medium size, it implies that there is a prevalence of companies falling within this size range. This finding can lead to several interpretations and inferences. The dominance of medium-sized companies may indicate a balanced market landscape with a mix of both small and large competitors. 

```{r}
# Scatterplot of Salary and Company Size
ggplot(df, aes(x = company_size, y = salary)) +
  geom_point(color = "steelblue") +
  labs(title = "Salary vs Company Size", x = "Company Size", y = "Salary (USD)")
```

The scatterplot indicates that the medium sized companies have a lower salary range compared to small and large companies. The salary margins between employees is significantly lower when compared to other companies. 
