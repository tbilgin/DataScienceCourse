# Datei Hochladen

Finde den Happiness Dataset in github. Da klicke auf die Raw und kopiere den Link . Du wirst diesen Link nach unten in <> kopieren und dann die <> Zeichen löchen.

<img width="1135" alt="Bildschirmfoto 2023-10-11 um 11 22 50" src="https://github.com/tbilgin/DataScienceCourse/assets/26571015/854700b3-6316-4e12-9ef4-01d1d98008bf">

<img width="1159" alt="image" src="https://github.com/tbilgin/DataScienceCourse/assets/26571015/4a48edc0-15fb-4a9e-9141-05077b21bede">

```
install.packages("RCurl")            # Paket zum Herunterladen
library(RCurl)                       
x <- getURL("<>")                    # kopiere den Link hier
mydata <- read.table(text = x, header = T)
attach(mydata)                       
```   


# Korrelationen

Wir haben die Korrelationen mit den Durschnittswerten für jedes Land berechnet. Ihr habt diese auch in Hausaufgabenlösung:

Wichtig: Der Kode ist nicht komplett. Fülle zwischen <> und lösche <> 
```
data_per_land <- mydata %>%                                        
    group_by(<Was schreibt man hier so dass wir jährliche Durschnitte berechnen?>) %>%                         
    summarise_at(vars(<Schreib hier alle Faktore und Happiness, durch Kommas gentrennt>),            
                 list(avg = mean))  %>%  
    select(<Was schreibt man hier so dass Ländername löschen?>)
```

Jetzt haben wir ein Dataset für Durschnittswerte. Damit möchten wir unsere lineare Regression Modellen bilden. Ergänze die felhlende Teile.
```
trend<-lm(Happiness_avg ~ LogGDPpercapita_avg, data = <welchen Dataset benutzen wir?>)
LogGDPpercapita_r2 <- summary(trend)$adj.r.squared

trend<-lm(Happiness_avg ~ <Welcher Faktor passt hier?>, data = <welchen Dataset benutzen wir?>)
Socialsupport_r2 <- summary(trend)$adj.r.squared

trend<-lm(Happiness_avg ~ <Welcher Faktor passt hier?>, data = <welchen Dataset benutzen wir?>)
Healthylifeexpectancyatbirth_r2 <- summary(trend)$adj.r.squared

trend<-lm(Happiness_avg ~ <Welcher Faktor passt hier?>, data = <welchen Dataset benutzen wir?>)
Freedomtomakelifechoices_r2 <- summary(trend)$adj.r.squared

trend<-lm(Happiness_avg ~ <Welcher Faktor passt hier?>, data = <welchen Dataset benutzen wir?>)
Generosity_r2 <- summary(trend)$adj.r.squared

trend<-lm(Happiness_avg ~ <Welcher Faktor passt hier?>, data = <welchen Dataset benutzen wir?>)
Perceptionsofcorruption_r2 <- summary(trend)$adj.r.squared

r2 <- c(LogGDPpercapita_r2, Socialsupport_r2, Healthylifeexpectancyatbirth_r2, Freedomtomakelifechoices_r2, Generosity_r2, Perceptionsofcorruption_r2)

r <- sqrt(r2)
r
```
Wie sehen die Werte aus? Etwas ist falsch, nicht?


Schau mal wieder an die Trendlinie für die Corruption:
```
lm(Happiness_avg ~ Perceptionsofcorruption_avg, data = data_per_land)
```
Zum korrigieren, können wir so was machen:
```
r[6] <- -r[6]
r
```
Jetzt zum Plot:
```
par(mai=c(1,3,1,1))
barplot(rev(r),las=1, names.arg = colnames(mydata)[9:4], horiz = T)
```
Schauen wir mal auf die Plots für das Einkommen:

```
par(mfrow=c(2,1))
trend<-lm(<Was schreibt man hier Trendlinie?>)
plot(LogGDPpercapita_avg, Happiness_avg)
abline(trend,col="blue")

trend<-lm(<Was schreibt man hier Trendlinie?>))
plot(LogGDPpercapita, Happiness)
abline(trend,col="blue")

```
<img width="415" alt="Bildschirmfoto 2023-10-06 um 13 00 50" src="https://github.com/tbilgin/DataScienceCourse/assets/26571015/87ea46af-11f1-4fc3-818a-5014fcfd9fd9">

Was ist der Grund für den Unterschied, denkst du?













