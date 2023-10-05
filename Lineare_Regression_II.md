# Datei Hochladen

Finde den Happiness Dataset in github. Da recht-klicke auf die Raw und wähle aus Link kopieren. D u wirst diesen Link nach unten in <> kopieren.


<img width="1144" alt="Bildschirmfoto 2023-10-05 um 15 40 11" src="https://github.com/tbilgin/DataScienceCourse/assets/26571015/d25688aa-9af9-4c2d-a4b3-6f82b2da45bb">


```
install.packages("RCurl")            # Paket zum Herunterladen
library(RCurl)                       
x <- getURL("<>")                    # kopiere den Link hier
mydata <- read.table(text = x, header = T)
attach(mydata)                       
```   


# Korrelationen

Wir haben gefunden, dass die Korrelationen höher sind, wenn sie mit den jährlichen Durschnittswerten berechnet sind. Warum ist das so? Schauen wir mal auf die Plots:

```
plot(LogGDPpercapita, Happiness)

