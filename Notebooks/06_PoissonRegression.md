
# Poisson Regression

```
install.packages("COUNT")
library(COUNT)
library(ggplot2)
library(tidyverse)
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


# Hausaufgabe

Führe geeignete Regression Analyse für die andere Variablen durch und zeichne die Plots.

Zuerst möchten wir sehen, wie die Korrelationen in dem Datensatz verteilt sind.
```
plot(fishing)
```
![image](https://github.com/tbilgin/DataScienceCourse/assets/26571015/5260f9bc-9864-4542-9bfb-ce0590dd1786)

## Mögliche Antwort 1: lineares Modell, plot mit base R

Wir werden ein lineares Modell zwischen Dichte (density) und der Anzahl Fische (totabund) bilden.
```
dichte_anzahl=lm(totabund ~ density, data = fishing)
summary(dichte_anzahl)

plot(fishing$density, fishing$totabund)
lines(fishing$density,predict(dichte_anzahl), col="orange", lwd = 4)
```
<img width="664" alt="image" src="https://github.com/tbilgin/DataScienceCourse/assets/26571015/c7438c22-4403-45e8-b4e6-c77ccd46f07d">

![image](https://github.com/tbilgin/DataScienceCourse/assets/26571015/2a5ff02d-db49-4da0-8ca9-53ff19e233af)

## Mögliche Antwort 2: Poisson Regression, ggplot

Wir werden eine Poisson Regression zwischen Ort (site) und der gefegten Fläche (sweptarea) modellieren.

```
summary(glm(totabund ~ sweptarea, data = fishing, family = poisson))

ggplot(fishing, aes(site, sweptarea)) +
  geom_point(alpha = 0.2) +
  geom_smooth(method = "glm", method.args = list(family = "poisson"))
```
summary(glm(totabund ~ sweptarea, data = fishing, family = poisson))
![image](https://github.com/tbilgin/DataScienceCourse/assets/26571015/2218dad3-e161-44b8-adb7-dc646e31c99c)

<img width="751" alt="Bildschirmfoto 2023-12-15 um 15 34 02" src="https://github.com/tbilgin/DataScienceCourse/assets/26571015/bdc97ba5-c4e2-4cd9-b940-b85b7ca901b9">

# Mögliche Antwort 3: Logistiche Regression, ggplot und tidyR

Wir werden eine logistische Regression zwischen Jahr (year) und dem Zeitraum (period) modellieren, wo wir uns damit entscheiden, ob das Jahr vor kurzem war oder nicht. Nur so dass, wir eine perfekte logistische Anpassung, wie hier, erkennen dürfen.

```
glm(period ~ year, data = fishing, family = binomial)

fishing %>%
  mutate(vor_kurzem = ifelse(period == "2000-2002", 1, 0)) %>%
  ggplot(aes(year, vor_kurzem)) +
  geom_point(alpha = 0.2) +
  geom_smooth(method = "glm", method.args = list(family = "binomial"))
```
![Bildschirmfoto 2023-12-15 um 16 06 31](https://github.com/tbilgin/DataScienceCourse/assets/26571015/afcb84c8-f5a7-4eea-bf7a-a73c50ce0ccc)
![image](https://github.com/tbilgin/DataScienceCourse/assets/26571015/a649be81-b1ff-4fdf-9f17-7d61b05504cf)








