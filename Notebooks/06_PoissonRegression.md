
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






