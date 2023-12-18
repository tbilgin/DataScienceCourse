# PCA

Pakete für PCA:
```
library(ggplot2)
library(tidyverse)
install.packages("ggfortify")
library(ggfortify)
```
ggfortify ist zum Zeichnen.

## Beispiel 1: Iris Datensatz (R Datensatz)
```
iris_pca <- prcomp(iris[,1:4])
autoplot(iris_pca, data = iris, colour = 'Species',
         loadings = TRUE, loadings.colour = 'blue',
         loadings.label = TRUE,loadings.label.size=3)
```
![image](https://github.com/tbilgin/DataScienceCourse/assets/26571015/7a44c9c1-fc36-4d0b-9a56-8c001717e496)


## Beispiel 2: Fishing Datensatz (R Datensatz in einem Paket)
```
install.packages("COUNT")
library(COUNT)
data(fishing)

s.fish=scale(fishing[,0:3]) # erste vier numerische Werte
fish.pca <- prcomp(s.fish)
autoplot(fish.pca, data = s.fish,
         loadings = TRUE, loadings.colour = 'blue',
         loadings.label = TRUE,loadings.label.size=3)
```
![image](https://github.com/tbilgin/DataScienceCourse/assets/26571015/2ff52ecc-5fac-4f3a-9f1f-9b3fdbbc50fd)



## Beispiel 3: Happiness Datensatz
```
# Read the CSV file into a data frame
happiness <- read.csv("happiness", sep="")
# Filter data for the year 2008
happiness1 <- happiness %>% filter(Year == 2008)
# Perform PCA
happy_pca <- prcomp(select(happiness1, 3:9))
# Plot
autoplot(happy_pca, data = select(happiness1, 3:9),
         loadings = TRUE, loadings.colour = 'blue',
         loadings.label = TRUE,loadings.label.size=3)
```
![image](https://github.com/tbilgin/DataScienceCourse/assets/26571015/54ba4809-f751-42c0-b092-e5d2050e1535)



