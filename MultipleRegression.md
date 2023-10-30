# Iris Dataset Entdecken
```
library(tidyverse)
head(iris)
glimpse(iris)
summary(iris)
plot(iris)
attach(iris)
```

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

Mach den Test mal für alle andere Variable. Haben sie auch eine normale Verteilung? Kannst du die Histograms als Subplots eines grossen Plots zeichnen?

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
dev.off()
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

# Gruppieren nach der Blumenart

```
ggplot(iris,aes(x=Petal.Length,y=Petal.Width, col = Species)) +	
  geom_point() + 
  geom_smooth(method="lm")
```
<img width="554" alt="Bildschirmfoto 2023-10-16 um 17 00 47" src="https://github.com/tbilgin/DataScienceCourse/assets/26571015/415e63ac-9f4a-43b6-b00d-f604b4b71d28">

Mach das für die Sepals jetzt!
```
ggplot(iris,aes(x=Sepal.Length,y=Sepal.Width, col = Species)) +	
  geom_point() + 
  geom_smooth(method="lm")
```
<img width="557" alt="Bildschirmfoto 2023-10-16 um 17 01 35" src="https://github.com/tbilgin/DataScienceCourse/assets/26571015/d849f2e3-78a9-4e8f-92e4-4d90f991c9a4">

Sieht so aus, dass die Weiten nicht nur ab Längen hängen aber auch ab der Blumenart ab.
Wie ist es mit Längen und Blumenarten? Benutzen wir dieses mal die Boxplots.

# Boxplot mit ggplot

```
ggplot(iris, aes(x = Species, y = Sepal.Length)) +
  geom_boxplot()
```
<img width="563" alt="Bildschirmfoto 2023-10-16 um 17 08 43" src="https://github.com/tbilgin/DataScienceCourse/assets/26571015/f1d9bf0c-d640-49ef-848d-63d2867a76b9">

Probiere es jetzt mit Petals:
```
ggplot(iris, aes(x = Species, y = Petal.Length)) +
  geom_boxplot()
```
<img width="562" alt="Bildschirmfoto 2023-10-16 um 17 09 23" src="https://github.com/tbilgin/DataScienceCourse/assets/26571015/ad38945a-e250-4410-9f5a-76f0f5f60112">

Die Längen hängen auch ab der Blumensart.

# Multiple Regression

Für Petal Weiten:
```
petal_width.trend = lm(Petal.Width ~ Species + Petal.Length + Sepal.Width + Sepal.Length, data = iris)
summary(petal_width.trend)
```
<img width="744" alt="Bildschirmfoto 2023-10-16 um 17 19 08" src="https://github.com/tbilgin/DataScienceCourse/assets/26571015/c654240d-6f34-437d-a34a-1f5dfcf9ed16">


Mit Blumenart sehen wir die Bestimmtheitsmass nicht. Das Model liest das als ein Text. Was können wir machen?

```
petal_width.trend = lm(Petal.Width ~ as.numeric(Species) + Petal.Length + Sepal.Width + Sepal.Length, data = iris)
summary(petal_width.trend)
```
<img width="742" alt="Bildschirmfoto 2023-10-16 um 17 17 07" src="https://github.com/tbilgin/DataScienceCourse/assets/26571015/da498957-65b6-450a-9fd6-3dc93ed4da90">

Probiere jetzt das für Petal Längen, Sepal Weiten und Sepal Längen:

```
petal_length.trend = lm(Petal.Length ~ as.numeric(Species) + Petal.Width + Sepal.Width + Sepal.Length, data = iris)
summary(petal_length.trend)
```
<img width="721" alt="Bildschirmfoto 2023-10-16 um 17 28 03" src="https://github.com/tbilgin/DataScienceCourse/assets/26571015/dd420330-3f49-428e-b4bc-27089b4f4b7c">

```
sepal_width.trend = lm(Sepal.Width ~ as.numeric(Species) + Sepal.Length + Petal.Width + Petal.Length, data = iris)
summary(sepal_width.trend)
```
<img width="715" alt="Bildschirmfoto 2023-10-16 um 17 30 02" src="https://github.com/tbilgin/DataScienceCourse/assets/26571015/e8c8767c-67f3-4963-8887-b013e1c5db72">

```
sepal_length.trend = lm(Sepal.Length ~ as.numeric(Species) + Sepal.Width + Petal.Width + Petal.Length, data = iris)
summary(sepal_length.trend)
```

<img width="708" alt="Bildschirmfoto 2023-10-16 um 17 36 24" src="https://github.com/tbilgin/DataScienceCourse/assets/26571015/1f539f56-ddf8-4f78-b1f6-8d880bb41528">










