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

```
Probiere das jetzt mit anderen Faktoren.


Was sind die Dimensione, wie lang und wie breit ist das Dataset?
```

```
Wie viele Länder sind in unserem Dataset?

```

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
par(mai=c())
barplot(1:6,las=1, names.arg = colnames(mydata)[4:9], horiz = T)
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
