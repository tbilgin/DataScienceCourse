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
Schauen wir mal an die Verteilungen, die due gesammelt hast. Beachte darauf, dass die Werten numerik sein müssen.
Falls du die noch hast. 
Ihr könnt auch in 2-3 Personen Gruppen bearbeiten. 
Sonst einfach benutze die Grössen Dataset, die ich letzte Woche gesammelt hab.


Schreibe deine Werte drin, durch Kommas gentrennt:

```
verteilung = c()
```
Berechne die gängigste Masszahle für deine Verteilung und dann zeichne sie. Probiere für deine Verteilung, wie viele breaks passen am besten.

<img width="1072" alt="Bildschirmfoto 2023-10-12 um 08 42 22" src="https://github.com/tbilgin/DataScienceCourse/assets/26571015/9aff29e0-2811-4c99-9c3d-e177332f5c2a">

<img width="798" alt="Bildschirmfoto 2023-10-12 um 08 43 02" src="https://github.com/tbilgin/DataScienceCourse/assets/26571015/99d87288-6204-4e0a-b707-8de1f8635eac">

Wie soll ich die Verteilung erstellen?

```
Verteilung = c(0,1,9,3,6,1,0)
hist(Verteilung)
```
<img width="410" alt="Bildschirmfoto 2023-10-12 um 08 44 06" src="https://github.com/tbilgin/DataScienceCourse/assets/26571015/18ee6edf-6cec-4c7b-aa78-a71d44ae377e">

Hmm etwas ist falsch. 🤔
```
Verteilung = c(155, 165, 165, 165, 165, 165, 165, 165, 165, 165, 175, 175, 175, 185, 185, 185, 185, 185, 185, 195 )
hist(Verteilung)
```
<img width="408" alt="Bildschirmfoto 2023-10-12 um 08 47 05" src="https://github.com/tbilgin/DataScienceCourse/assets/26571015/4e915775-073f-491c-9154-5ffd7ddddec1">

Jetzt richtig.

Viele Wege möglich:
```
mean(Verteilung)
```
<img width="74" alt="Bildschirmfoto 2023-10-12 um 09 47 25" src="https://github.com/tbilgin/DataScienceCourse/assets/26571015/fe41d29c-efe9-49d6-954d-fdcf5e5834e8">

```
c(173.5, 173.5, 173.5, 173.5, 173.5, 173.5, 173.5, 173.5, 173.5, 173.5)
```
oder so:
```
c(mean(Verteilung),mean(Verteilung), mean(Verteilung), mean(Verteilung), mean(Verteilung), mean(Verteilung), mean(Verteilung), mean(Verteilung), mean(Verteilung), mean(Verteilung))
```
eine bessere Idee?
```
rep(mean(Verteilung), 10)
```
<img width="464" alt="Bildschirmfoto 2023-10-12 um 09 50 13" src="https://github.com/tbilgin/DataScienceCourse/assets/26571015/6cd8fa6e-2d5f-459a-be43-e33a26feaa6a">









