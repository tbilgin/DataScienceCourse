# Logistische Regression
```
install.packages("mlbench")
data("PimaIndiansDiabetes2", package = "mlbench")
```

```
head(PimaIndiansDiabetes2)
glimpse(PimaIndiansDiabetes2)
```
```
apply(PimaIndiansDiabetes2[,1:8], 2, shapiro.test)
```
```
diabetes.data <- na.omit(PimaIndiansDiabetes2)
```
```
diabetes.data %>%
  mutate(prob = ifelse(diabetes == "pos", 1, 0)) %>%
  head()
```
```
diabetes.data %>%
  mutate(prob = ifelse(diabetes == "pos", 1, 0)) %>%
  glimpse()
```

```
diabetes.data %>%
  mutate(prob = ifelse(diabetes == "pos", 1, 0)) %>%
  ggplot(aes(glucose, prob)) +
  geom_point(alpha = 0.2)
```
```
model <- glm( diabetes ~., data = diabetes.data, family = binomial)
summary(model)
```
```
diabetes.data %>%
  mutate(prob = ifelse(diabetes == "pos", 1, 0)) %>%
  ggplot(aes(glucose, prob)) +
  geom_point(alpha = 0.2) +
  geom_smooth(method = "glm", method.args = list(family = "binomial")) +
  labs(
    x = "Glukose",
    y = "Diabetes"
  )
```
```
exp(summary(model)$coeff[,1])
```
# Poisson Regression

```
install.packages("COUNT")
library(COUNT)
data(fishing)
```
```
summary(glm(totabund ~ meandepth, data = fishing, family = poisson))
```
```
ggplot(fishing, aes(meandepth, totabund)) +
  geom_point(alpha = 0.2) 
```
```
ggplot(fishing, aes(meandepth, totabund)) +
  geom_point(alpha = 0.2) +
  geom_smooth(method = "glm", method.args = list(family = "poisson"))
```






