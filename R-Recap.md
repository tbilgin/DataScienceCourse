# Skripte für R-Recap

## Einführung und Entdeckung vom Dataset

Wir werden das Datai zuerst hochladen und schauen schnell, wie es aussieht: 
```
mydata = read.table("happiness", header = T)
attach(mydata)
head(mydata)
```
Welche Werte haben die Faktoren?
```
apply(mydata[,3:9], 2, mean)
```
Falls ich nur Happiness-Werte sehen möchte?
```
Happiness
```
Probiere das jetzt mit anderen Faktoren.


Was sind die Dimensione, wie lang und wie breit ist das Dataset?
```
dim(mydata)
```
Wie viele Länder sind in unserem Dataset?

```
unique(Countryname)
```

## Welche Faktoren spielen die grösste Rolle in Happiness?

Zuerst sehen wir mal das Figur:
```
plot(mydata)
```
Werden wir unglücklicher mit der Zeit?
```
cor.test(Happiness, Year, method = "spearman")
```
Ok, jeder berechnet einen Korrelationskoeffizient so dass wir ein Figur machen können:
```
cor.test(Happiness, LogGDPpercapita, method = "spearman")
cor.test(Happiness, Socialsupport, method = "spearman")
cor.test(Happiness, Healthylifeexpectancyatbirth, method = "spearman")
cor.test(Happiness, Freedomtomakelifechoices, method = "spearman")
cor.test(Happiness, Generosity, method = "spearman")
cor.test(Happiness, Perceptionsofcorruption, method = "spearman")
```
Die Rho-Werte sind die Korrelationskoeffiziente. Also die sagen uns die Rolee jede Faktor auf die Glücklichkeit spielt. Jetzt zeichnen wir mal das Figur:
```
par(mai=c(1,3,1,1))
barplot(c(-0.31, 0.15, 0.51, 0.78, 0.76, 0.79),las=1, names.arg = colnames(mydata)[9:4], horiz = T)
```

# Hausaufgabe
```
install.packages('tidyverse')
library(tidyverse)
```

Hier ist ein Beispiel. 
```
mydata %>% count(Year, wt = Generosity)
```
Antworte die untene Fragen:
1) Wie ist diese Zeile benutzbar? Was könnte die Frage sein? Und die Hypothese?
2) Stelle zwei andere Fragen, die du mit tidyverse antworten kannst.
3) Was sind deine Hypothesen für deine Fragen?
4) Schreib dein Skript mit mindestens ein tidyverse Zeile per Hypothese
5) In welchen Aspekten findest du tidyverse hilfreich? Wir hatten zwei gennant in der Präsentation. Finde noch 1-2 ud erkläre warum basierend auf deine Skripte.



## Weitere Beispiele

Beschreibe was die untene Koden machen: 
```
mydata  %>%  filter(Countryname == "Switzerland" & Year > 2010) %>% group_by(Year)
```
<img width="799" alt="Bildschirmfoto 2023-09-27 um 10 32 50" src="https://github.com/tbilgin/DataScienceCourse/assets/26571015/47adbeaf-e4f1-41a6-a28c-d4bf3470b3d5">

```
mydata  %>%  group_by(Countryname, Year)
```
<img width="790" alt="Bildschirmfoto 2023-09-27 um 10 35 22" src="https://github.com/tbilgin/DataScienceCourse/assets/26571015/369d13f5-f6f0-43e1-a76e-af83122255a0">

```

mydata %>% group_by(Countryname) %>%  select(-(LogGDPpercapita:Generosity)) %>% filter(Perceptionsofcorruption == min(Perceptionsofcorruption))

```
<img width="418" alt="Bildschirmfoto 2023-09-27 um 10 37 19" src="https://github.com/tbilgin/DataScienceCourse/assets/26571015/df690d2e-9efe-41a6-938a-6180232f3124">

```
mydata %>% group_by(Countryname) %>% summarise(avg_GDP = mean(LogGDPpercapita), st_dev = sd(LogGDPpercapita))
```
<img width="308" alt="Bildschirmfoto 2023-09-27 um 10 39 05" src="https://github.com/tbilgin/DataScienceCourse/assets/26571015/638c953c-47d7-400c-a4c5-40c05c8b1f26">


Tip für die letzte Frage: Dank zu tidyverse haben wir hier unser Dataset mehr 'tidy' gemacht und subsetting, filtering etc waren dann sehr einfach zu kodieren, und auch lesbar ;)  


Lese hier für mehr: http://cbdm-01.zdv.uni-mainz.de/~galanisl/danalysis/index.html

