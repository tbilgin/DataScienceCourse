# Gängigste Masszahle

Diese Befehle geben die gängigste Masszahle für eine Verteilung. Ich werde diese für Haappines data machen.
```
install.packages("RCurl")            # Paket zum Herunterladen
library(RCurl)                       
x <- getURL("<>")                    # kopiere den Link vom row data Seite von Happiness, lösche die <>
mydata <- read.table(text = x, header = T)
attach(mydata)  

mean(Happiness)
max(Happiness)
min(Happiness)
sd(Happiness)
```

Wir können auch einfach diesen Befehl benutzen:

```
summary(Happiness)
```
<img width="333" alt="Bildschirmfoto 2023-10-11 um 11 00 16" src="https://github.com/tbilgin/DataScienceCourse/assets/26571015/5629421d-981c-4369-ae7c-a8327ba40df2">

Somit zeichnet man eine Verteilung:
```
hist(Happiness)
```
<img width="388" alt="Bildschirmfoto 2023-10-11 um 11 02 47" src="https://github.com/tbilgin/DataScienceCourse/assets/26571015/3a22fe14-1205-4120-b178-5d2d20fefa2e">


Mit dem Parameter breaks kannst du mehr Bars erhalten. Probiere, wie viele breaks passen am besten?
```
hist(verteilung, breaks = 5)
```

# Aufgabe
Schauen wir mal an die Verteilungen, die due gesammelt hast. Beachte darauf, dass die Werten numeric sein müssen.
Falls du die noch hast. 
Ihr könnt auch in 2-3 Personen Gruppen bearbeiten. 
Sonst einfach benutze einen anderen Faktor vom Happiness Dataset.


Schreibe deine Werte drin, durch Kommas gentrennt:

```
verteilung = c()
```

Diese Befehle geben die gängigste Masszahle für deine Verteilung:
```
mean(verteilung)
max(verteilung)
min(verteilung)
sd(verteilung)
```
Somit zeichnet man eine Verteilung:
```
hist(verteilung)
```
Mit dem Parameter breaks kannst du mehr Bars erhalten. Probiere für deine Verteilung, wie viele breaks passen am besten?
```
hist(verteilung, breaks = 5)
```


