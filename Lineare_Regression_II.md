# Datei Hochladen

Finde den Happiness Dataset in github. Da recht-klicke auf die Raw und wähle aus Link kopieren. Du wirst diesen Link nach unten in <> kopieren.


<img width="1144" alt="Bildschirmfoto 2023-10-05 um 15 40 11" src="https://github.com/tbilgin/DataScienceCourse/assets/26571015/d25688aa-9af9-4c2d-a4b3-6f82b2da45bb">


```
install.packages("RCurl")            # Paket zum Herunterladen
library(RCurl)                       
x <- getURL("<>")                    # kopiere den Link hier
mydata <- read.table(text = x, header = T)
attach(mydata)                       
```   


# Korrelationen

Wir haben die Korrelationen mit den jährlichen Durschnittswerten berechnet. Ihr habt diese auch in Hausaufgabenlösung:

```
data_per_land <- mydata %>%                                        
    group_by(Countryname) %>%                         
    summarise_at(vars(LogGDPpercapita,Socialsupport, Healthylifeexpectancyatbirth,Freedomtomakelifechoices, Generosity, Perceptionsofcorruption, Happiness),            
                 list(avg = mean))  %>%  
    select(-Countryname)

summary(data_per_land)

trend<-lm(Happiness_avg ~ LogGDPpercapita_avg, data = data_per_land)
LogGDPpercapita_r2 <- summary(trend)$adj.r.squared

trend<-lm(Happiness_avg ~ Socialsupport_avg, data = data_per_land)
Socialsupport_r2 <- summary(trend)$adj.r.squared

trend<-lm(Happiness_avg ~ Healthylifeexpectancyatbirth_avg, data = data_per_land)
Healthylifeexpectancyatbirth_r2 <- summary(trend)$adj.r.squared

trend<-lm(Happiness_avg ~ Freedomtomakelifechoices_avg, data = data_per_land)
Freedomtomakelifechoices_r2 <- summary(trend)$adj.r.squared

trend<-lm(Happiness_avg ~ Generosity_avg, data = data_per_land)
Generosity_r2 <- summary(trend)$adj.r.squared

trend<-lm(Happiness_avg ~ Perceptionsofcorruption_avg, data = data_per_land)
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
Die Korrelationen sind höher. Warum ist das so? Schauen wir mal auf die Plots für das Einkommen:

```
par(mfrow=c(2,1))
trend<-lm(Happiness_avg ~ LogGDPpercapita_avg, data = Einkommen)
plot(LogGDPpercapita_avg, Happiness_avg)
abline(trend,col="blue")

trend<-lm(Happiness ~ LogGDPpercapita, data = mydata)
plot(LogGDPpercapita, Happiness)
abline(trend,col="blue")

```
<img width="415" alt="Bildschirmfoto 2023-10-06 um 13 00 50" src="https://github.com/tbilgin/DataScienceCourse/assets/26571015/87ea46af-11f1-4fc3-818a-5014fcfd9fd9">

Was ist der Grund für den Unterschied, denkst du?


# Verteilung

Schauen wir mal an die Verteilungen.









