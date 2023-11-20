# Semesterprüfung - Statistische Modellierung und Simulation HS23 AD22

Nachfolgend findest du die Prüfungsfragen sowie die Antworten und die Punkte zu jeder Frage. Antworten, die hier nicht geschrieben sind, können auch richtig bewertet werden und wurden schon in der Prüfung richtig bewertet. Bitte schaue dich dein Feedback im Moodle genau an. 

Fragen, die du mit einem Kode beantworten musst, sind durch ein [C] am Ende gekennzeichnet. Fragen, die du als Text mit einem print()-Befehl beantworten musst, werden mit einem [T] gekennzeichnet. Es ist nicht notwendig, Variablen in den Druckbefehl einzufügen. Das direkte Schreiben von Zahlen ist akzeptabel und was ich erwarte. Du kannst mehrere Sätze innerhalb der Klammern schreiben. zum Beispiel: print("Der p-Wert ist 0.7. Weil der Wert so gross/ klein ist, ist der Unterschied signifikant/nicht signifikant.")) Fragen, die beide Arten von Antworten erfordern, werden durch ein [CT] gekennzeichnet. Solche Antworten würden sowohl Kode als auch einen Text enthalten, den du mit einem Druckbefehl schreiben sollst. 

## A. Hochladen von den Daten (5 Punkte)

Du wirst einen Datensatz über Opossums bearbeiten. Opossums sind Beuteltiere, die nur in Amerika leben. Die Proben in diesem Datensatz wurden an verschiedenen Studienorten in Kanada gesammelt. Die Daten umfassen:
•	Probennummer
•	den Studienort
•	Herkunft der Population
•	Geschlecht
•	Alter
•	Kopflänge in mm
•	Schädelbreite in mm
•	Gesamtlänge des Körpers in cm
•	Schwanzlänge in cm
•	Fusslänge
•	Länge der Ohrmuschel
•	Augenabstände
•	Brustumfang in mm
•	Bauchumfang in mm

Du kannst die Daten unter diesem Link finden: https://github.com/tbilgin/marc/blob/main/possum.csv

1) Lade die Daten mit den folgenden Befehlen in Ihr R-Studio hoch. Füge den Link zu den Rohdaten innerhalb der Paranthese ein. [C] 5 Punkte
```
install.packages("RCurl")            
library(RCurl)                       
x <- getURL("https://raw.githubusercontent.com/tbilgin/marc/main/possum.csv")
possum <- read.table(text = x, header = T)
```

## B. Erkundung der Daten (25 Punkte)

1) Wie kann man den Mittelwert, den Median und alle Quartilwerte für jede Spalte sehen? [C] 3 Punkte
```
summary(possum)
```

2) Was passiert, wenn man versucht, das Alter des ältesten Opossums in der Studie zu bestimmen? Verwenden Sie den Befehl print, um das zu erklären. [CT] 9 Punkte
```
max(possum$age)
print("Wir sehen, dass diese Spalte NA's hat, d.h. unbekannte Werte")
# Wenn die Studierende den Befehl attach() verwenden würden, sähe die Antwort wie folgt aus: max(age)
# Diese Variationen, die sich aus dem Befehl attach() ergeben, gelten für die gesamte Prüfung.
```

3) Von wie vielen einzelnen Studienstandorten werden die Daten gesammelt? [C] 6 Punkte
```
length(unique(possum$site)) 
# Nur unique(site) ist auch richrig, wenn man dann mit print() die richtige Antwort schreibt. Aber ohne print ist die Antwort dann unvollständig. 
# Die Verwendung des Befehls "max(site)" würde ebenfalls Teilpunkte bringen. 
```

4) Ermittle das Durchschnittsalter für jeden Untersuchungsort mit tidy R. [C] 7 Punkte
```
possum %>% group_by(site) %>% summarise(mean(age))
```

## C. Auswirkung des Alters

1) Führe eine Regressionsanalyse durch, um herauszufinden, um wie viele mm der Kopf eines Opossums mit jedem Alter länger wird. Gib das Wachstum der Kopflänge pro Alter mit dem Druckbefehl an.  [CT] 11 Punkte 
```
lm(hdlngth ~ age, data = possum)
print("Sie beträgt 0.59.")
```

2) Erstelle eine scatter plot mit base R und füge die best-fit-Linie hinzu. [C] 12 Punkte
```
plot(hdlngth ~ age, data = possum)
abline(lm(hdlngth ~ age, data = possum))
```

3) Ermittle das Bestimmtheitsmass und gib das mit dem Druckbefehl aus. Findest du, dass das Alter die Variation der Kopflänge gut erklärt? [T] 6 Punkte
```
print("Das Bestimmtheitsmass beträgt 0.1, also niedrig. Das Alter erklärt die Kopflänge noch signifikant aber nicht viel.")
```

4) Denkst du aufgrund dieses Bestimmtheitsmasses und des Diagramms, dass eine lineare Anpassung hier die beste Lösung ist? Überlege in deiner Antwort, wie das Bestimmtheitsmass berechnet wird und wie die Residuen im Diagramm verteilt sind. [T] 6 Punkte
```
print("Das Alter erklärt die Kopflänge nicht so gut. Wir berechnen das Bestimmtheitsmass, indem wir die Abstände zwischen jedem Rückstand und der Linie addieren. Bei den niedrigeren Alterswerten sind die Variation/Abweichungen und damit dieser Abstand sehr hoch. Deswegen ist das Bestimmtheitsmass nicht hoch. Das sieht man auch im Graph. Deswegen ist eine lineare Anpassung nicht die beste Lösung.")
```
 
## D. Auswirkungen von Geschlecht und anderen

1) Stelle die Kopflängenverteilungen für männliche und weibliche Opossums mit ggplot dar. [C] 7 Punkte
```
ggplot(possum, aes(x=hdlngth, color = sex)) + geom_density()
```

2) Unterscheiden sich die Kopflängen von männlichen und weiblichen Opossums statistisch voneinander? Berechne die 95% Konfidenzintervalle für deine Antwort. Erkläre das Ergebnis mit dem Druckbefehl. Erkläre das Ergebnis mit dem Druckbefehl. [CT] 15 Punkte
```
kopf.länge.m = hdlngth[sex == 'm']
kopf.länge.f = hdlngth[sex == 'f']

mean(kopf.länge.m) + 1.96 * sd(kopf.länge.m) / sqrt(length(kopf.länge.m))
mean(kopf.länge.m) - 1.96 * sd(kopf.länge.m) / sqrt(length(kopf.länge.m))

mean(kopf.länge.f) + 1.96 * sd(kopf.länge.f) / sqrt(length(kopf.länge.f))
mean(kopf.länge.f) - 1.96 * sd(kopf.länge.f) / sqrt(length(kopf.länge.f))

print ("Die Kopflängen von männlichen und weiblichen Opossums unterscheiden sich nicht statistisch voneinander, weil die konfidenzintervallen überschneiden sich.")

# Studierende dürfen hier entweder base R oder tidy R benutzen.

```

3)  Prüfen wir, ob die numerische Faktoren in Daten zur Erklärung der Körperlänge beitragen. Führe dazu eine multiple lineare Regressionsanalyse durch. [C] 8 Punkte
```
summary(lm(totlngth ~ hdlngth + skullw + taill + age + site +
             footlgth + earconch + eye + chest +
             belly, data = possum))
```

4) Welche numerischen Faktoren tragen dazu bei, die Variation der Gesamtkörperlänge signifikant zu erklären? Gib deine Antwort mit dem Druckbefehl. [T] 5 Punkte
```
print("Kopflänge, Schwanzlänge und Studienort")
```

# Alternative Fragen

Benutze den Befehl 'glimpse()' um zu verstehen, welche der Spalten den Datentyp 'character' haben. Melde deine Antwort mit dem Befehl 'print()'. [CT]
```
glimpse(possum)
print("Pop und sex, also Population und Geschlecht")
```
Du wirst feststellen, dass auf einem Untersuchungsort Angaben zum Alter fehlen. Um welchen Untersuchungsort handelt es sich? Gib deine Antwort mit dem Befehl print bekannt. [T]
```
print("im zweiten Untersuchungsort")
```
Da wir sehen wollen, wie viele Datenpunkte fehlen, filtern wir alle anderen Untersuchungsor mit vollständigen Altersdaten heraus und drucken die Alterswerte nur von dem Untersuchungsort mit den fehlenden Daten. Verwende dazu tidy R. Melde dann, wie viele Datenpunkte fehlen, indem du den Druckbefehl verwendest. [CT]
```
possum %>% filter(site==2) %>% select(age)
print("Es gibt zwei fehlende Datenpunkte.")
```
Um die NA-Werte zu ersetzen, hast du beschlossen, sich die Kopflängenverteilungen für verschiedene Altersgruppen anzuschauen. Erstelle einen Boxplot mit ggplot. Färbe die Kästchen entsprechend dem Alter. [C]
```
ggplot(possum, aes(x = as.factor(age), y = hdlngth)) +
  geom_boxplot(aes(fill=as.factor(age)))
# Studierende dürfen auch den Datentyp von age ändern: 1) possum$age = as.factor(possum$age). Beachte dass, age = as.factor(age) würde nicht klappen, würde aber noch Teilpunkte bekommen.
```
Bei welcher Altersgruppe ist die Kopflängenverteilung am ehesten mit der der NA-Gruppe vergleichbar? Gib deine Antwort mit einem Druckbefehl an. [T]
```
print("Alter eins scheint dem am nächsten zu sein.")
```
Nun ersetze die fehlenden Altersdaten durch das Alter, das du oben als am nächsten liegend ermittelt hast. Verwende den Befehl is.na(), um die Indizes der fehlenden Daten zu ermitteln.  [C]
```
possum$age[is.na(possum$age)] = 1
# Studierende dürfen hier auch direkt age statt possum$age benutzen falls sie den attach Befehl verwendet haben. 
```
Wie kannst du das Ergebnis über den Studienort erklären? [T]
```
print("Das bedeutet, dass Opossums, die aus verschiedenen Gebieten stammen, sich in ihrer Grösse unterscheiden.")
```


