# Iris Dataset Entdecken
```
library(tidyverse)
head(iris)
glimpse(iris)
summary(iris)
plot(iris)
attach(iris)
``

<img width="449" alt="Bildschirmfoto 2023-10-16 um 16 16 28" src="https://github.com/tbilgin/DataScienceCourse/assets/26571015/b471e889-cf13-4b1c-bbe9-032654da9ab8">
<img width="911" alt="Bildschirmfoto 2023-10-16 um 16 16 44" src="https://github.com/tbilgin/DataScienceCourse/assets/26571015/fb428f7d-e0af-470d-a04f-b685fe6c706a">
<img width="876" alt="Bildschirmfoto 2023-10-16 um 16 17 01" src="https://github.com/tbilgin/DataScienceCourse/assets/26571015/53c5fe06-75e7-43f0-ba85-1c14954164a8">
<img width="656" alt="Bildschirmfoto 2023-10-16 um 16 17 37" src="https://github.com/tbilgin/DataScienceCourse/assets/26571015/e6957dd0-e111-4fae-8c0e-b6b41de1f7f2">

# Verteilungen

```
hist(Sepal.Width)
shapiro.test(Sepal.Width)
```
<img width="672" alt="Bildschirmfoto 2023-10-16 um 16 30 41" src="https://github.com/tbilgin/DataScienceCourse/assets/26571015/c802d5ba-f29c-460a-bf0d-25763d72753e">
<img width="420" alt="Bildschirmfoto 2023-10-16 um 16 30 55" src="https://github.com/tbilgin/DataScienceCourse/assets/26571015/431dac4f-d0fb-43f7-a1b9-24d26891ea04">

Mach den Test mal für alle andere Variable. Haben sie auch eine normale Verteilung? Kannst du die Histograms als Subplots einer grossen Plot zeichnen?

```
par(mfrow = c(2, 2)) 
hist(Sepal.Width)
shapiro.test(Sepal.Width)
hist(Sepal.Length)
shapiro.test(Sepal.Length)
hist(Petal.Width)
shapiro.test(Petal.Width)
hist(Petal.Length)
shapiro.test(Petal.Length)
```

<img width="826" alt="Bildschirmfoto 2023-10-16 um 16 36 18" src="https://github.com/tbilgin/DataScienceCourse/assets/26571015/681745d1-aaa2-43c9-92d8-5a14a966da92">
<img width="400" alt="Bildschirmfoto 2023-10-16 um 16 38 29" src="https://github.com/tbilgin/DataScienceCourse/assets/26571015/07c9cc3f-de3d-43b1-aaca-6a03b4f6201b">
<img width="405" alt="Bildschirmfoto 2023-10-16 um 16 38 43" src="https://github.com/tbilgin/DataScienceCourse/assets/26571015/b60d66f6-4d14-4e04-b52e-c1e591c3ad49">


# Eine lineare Regression

```
plot(Petal.Length, Petal.Width)
summary(lm(Petal.Width ~ Petal.Length))
abline(lm(Petal.Width ~ Petal.Length))
```
<img width="705" alt="Bildschirmfoto 2023-10-16 um 16 22 15" src="https://github.com/tbilgin/DataScienceCourse/assets/26571015/9277e502-d3b0-4a84-8479-32a2fbfd217a">
<img width="700" alt="Bildschirmfoto 2023-10-16 um 16 45 30" src="https://github.com/tbilgin/DataScienceCourse/assets/26571015/93033957-2497-43d9-8e34-1ffef44aad5d">

Wir können die Konfidenzintervallen hineinfügen.

# GGPLOT (endlich!)
```
ggplot(iris,aes(x=Petal.Length,y=Petal.Width)) +	
  geom_point() + 
  geom_smooth(method="lm")
```
<img width="561" alt="Bildschirmfoto 2023-10-16 um 16 47 59" src="https://github.com/tbilgin/DataScienceCourse/assets/26571015/7eaa0706-79d4-4a5d-8225-80eb6784e304">

Mache das für die Sepals statt Petals.
```
summary(lm(Sepal.Width ~ Sepal.Length))
ggplot(iris,aes(x=Sepal.Length,y=Sepal.Width)) +	
  geom_point() + 
  geom_smooth(method="lm")
```
<img width="559" alt="Bildschirmfoto 2023-10-16 um 16 46 54" src="https://github.com/tbilgin/DataScienceCourse/assets/26571015/b3e1ae6e-77b4-4b07-bf76-cf150e7710c4">

<img width="725" alt="Bildschirmfoto 2023-10-16 um 16 46 29" src="https://github.com/tbilgin/DataScienceCourse/assets/26571015/9ed33eb0-10e9-4fbb-8478-159dcdd764cf">



