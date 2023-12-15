# Erklären die Variablen die Blumensarten? 

Dazu werden wir eine Multiple Regression für die Blumensarten durchführen. Man muss daran denken, dass die Blumensarten keine numerische Werte sind.

```
attach(iris)
species.trend = lm(as.numeric(Species) ~ Petal.Width + Petal.Length + Sepal.Width + Sepal.Length, data = iris)
summary(species.trend)
coefficients(species.trend)
```
<img width="701" alt="Bildschirmfoto 2023-10-20 um 14 31 42" src="https://github.com/tbilgin/InProgress/assets/26571015/0d7c6342-1411-4786-9c9e-a0b4ef20ae52">
<img width="716" alt="Bildschirmfoto 2023-10-20 um 14 31 59" src="https://github.com/tbilgin/InProgress/assets/26571015/463993b2-9a52-4445-b34a-6829257da472">

Was macht der Befehl coefficients, denkt ihr?

Was denkt ihr? Kann man die Blumensarten von Petal und Sepal Grössen einschätzen?
Welche sind statistisch signifikant? Wie weiss man das?


# Multiple Regression 

Datei Hochladen und Pakete installieren

```
install.packages("RCurl")            # Paket zum Herunterladen
library(RCurl)                       
x <- getURL("https://raw.githubusercontent.com/tbilgin/DataScienceCourse/main/happiness")                    # kopiere den Link vom row data Seite von Happiness, lösche die <>
mydata <- read.table(text = x, header = T)
attach(mydata)  
library(tidyverse)
```

Entdecken mit neu erlernten Befehlen
```
summary(mydata)
glimpse(mydata)
```

Wir brauchen die Ländernamen nicht.
```
mydata.nocountry = mydata %>%  
  select(-Countryname)
```

Testen wir mal, ob die Verteilungen normal sind. Wir werden apply Funktion verwenden.
```
apply(mydata.nocountry,2,shapiro.test)
```
Was denkt ihr?

Für die multiple Regression schreiben wir ein Formula. Hier ist es:
```
trend = lm(Happiness ~ LogGDPpercapita + Socialsupport + Healthylifeexpectancyatbirth + Freedomtomakelifechoices + Generosity + Perceptionsofcorruption)
summary(trend)
```
Welche Faktoren erklären die Glücklichkeit, denkst du?
<img width="891" alt="Bildschirmfoto 2023-10-20 um 15 02 53" src="https://github.com/tbilgin/InProgress/assets/26571015/fdee7934-493e-4243-bc54-c6a3cfc715ef">


Was würde passieren falls wir nur Einkommen benutzen?
```
trend.gdp = lm(Happiness ~ LogGDPpercapita)
summary(trend.gdp)
```
<img width="695" alt="Bildschirmfoto 2023-10-20 um 15 03 52" src="https://github.com/tbilgin/InProgress/assets/26571015/28a9b1e5-dbe8-44cf-a2bf-16b5d926da06">

Probiere irgendeine andere Kombination von Faktoren. Wie ändert das die totale Bestimmtheitsmasse?


Hier kann man auch wieder den Befehl coefficients benutzen.
```
coefficients(trend)
```
Und auch Konfidenzintervallen berechnen lassen:
```
confint(trend, level=0.95)
```











