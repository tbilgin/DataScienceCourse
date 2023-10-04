# Lineare_Regression
## Daten Herunter- und Hochladen 

Wir werden lernen wie man Daten direkt mit einem Link an R hochlädt.
```
install.packages("RCurl")            # Paket zum Herunterladen
library(RCurl)
x <- getURL("https://raw.githubusercontent.com/tbilgin/DataScienceCourse/main/happiness")
mydata <- read.table(text = x, header = T)
attach(mydata)                       # so dass die Spalten unabhängig bezeichnet sind
   
 ```  

## Datenanalyse mit Tidyverse

Schauen wir mal an die Beziehung zwischen Einkommen per capita und Glücklichkeit einer Nation.

```   
mydata %>%                                           # Datenauswahl               
group_by(Countryname) %>%                            # Gruppenauswahl
summarise_at(vars(LogGDPpercapita, Happiness),       # Spaltenauswahl
   list(avg = mean))                       # Funktion                   
```
<img width="374" alt="Bildschirmfoto 2023-09-27 um 12 18 45" src="https://github.com/tbilgin/DataScienceCourse/assets/26571015/87cc573b-9014-4bdd-b465-6eb417911cb4">

Wie kann man aber diese Beziehung visualisieren? Wir möchten dann nur die Spalten für Einkommen und Glücklichkeit:
```
mydata %>%                                        
group_by(Countryname) %>%                         
summarise_at(vars(LogGDPpercapita, Happiness),            
   list(avg = mean))  %>%  
select(-Countryname)
```   
<img width="312" alt="Bildschirmfoto 2023-09-27 um 14 04 12" src="https://github.com/tbilgin/DataScienceCourse/assets/26571015/3c61fa0a-35d1-4532-99d5-edb425b3fae5">

## Plot

Und jetzt alles drin plot()!

```  
plot(
mydata %>%                                        
group_by(Countryname) %>%                         
summarise_at(vars(LogGDPpercapita, Happiness),            
   list(avg = mean))  %>%  
select(-Countryname)
)
```  

<img width="207" alt="Bildschirmfoto 2023-09-27 um 14 05 57" src="https://github.com/tbilgin/DataScienceCourse/assets/26571015/b2f97f3a-94fc-43b4-867f-afb47248c08f">

## Regression

Für eine lineare Regression zu beschreiben, speichern wir mal zuerst alles unter Einkommen:

``` 
Einkommen <- mydata %>%                                        
    group_by(Countryname) %>%                         
    summarise_at(vars(LogGDPpercapita, Happiness),            
                 list(avg = mean))  %>%  
    select(-Countryname)
``` 

Und jetzt bilden wir das Model:

``` 
trend<-lm(Happiness_avg ~ LogGDPpercapita_avg, data = Einkommen)
```

Wie ist Einkommen anders als mydata? Liste jeden Unterschied. Welche Befehle helfen dir?



Nächst zeichnet man die Linie, die den Model beschreibt:

```
abline(trend,col="yellow")
```
<img width="214" alt="Bildschirmfoto 2023-09-27 um 14 46 14" src="https://github.com/tbilgin/DataScienceCourse/assets/26571015/bb488856-764c-4e13-bb98-1f3b0c082b3b">

Und wir können auch alles über die Regression mit diesem Befehl überfahren:
```
summary(trend)
```
<img width="505" alt="Bildschirmfoto 2023-09-27 um 15 19 17" src="https://github.com/tbilgin/DataScienceCourse/assets/26571015/c668b80a-827e-452d-8036-3d623181bfa5">

Hier ist -1.2678 der y-Achenabscnitt und 0.7254 ist die Steigung.
Bestimmheitsmass sagt uns wie gut die lienare Regression die Variation unserer Beobachtung erklärt. Es ist das Quadrat der Korrelation. Also dann wie berechnet man die Korrelation zwischen dem Einkommen und der Glücklichkeit einer Nation?





## Praktikum Partnerarbeit:

Probiere jetzt die Korrelation für einen anderen Faktor zu berechnen. Arbeite mit einem Partner:

Alles zwischen <> tausche mit dem richtigen Variablen aus.
### Schritt 1:

``` 
<Name des Faktors> <- mydata %>%                                        
    group_by(Countryname) %>%                         
    summarise_at(vars(<Faktor>, Happiness),            
                 list(avg = mean))  %>%  
    select(-Countryname)
``` 
### Schritt 2:


``` 
trend<-lm(Happiness_avg ~ <Faktor>_avg, data = <Faktor>)
abline(trend,col="<deine ausgewählte Farbe>")
summary(trend)
# berechne die Wurzel des Bestimmheitsmasses
```

# Hausaufgabe

Berechne die Korrelation zwischen der Glücklichkeit und allen Faktoren per Land. Zeichne das gleiche Figur von der letzten Woche und schau ob es Unterchiede gibt:

<img width="1045" alt="image" src="https://github.com/tbilgin/DataScienceCourse/assets/26571015/a1493c35-aab8-4f88-8635-d045207ef6e2">

# Hausaufgabe Lösung

Wir erstellen zuerst einen neuen Variabel, der alle Durschnitte für jeden Faktor hat. Beachte was ich im Kod geändert hab. Schau mal, wie der neue Variabel aussieht. Wie machst du das?
``` 
data_per_land <- mydata %>%                                        
    group_by(Countryname) %>%                         
    summarise_at(vars(LogGDPpercapita,Socialsupport, Healthylifeexpectancyatbirth,Freedomtomakelifechoices, Generosity, Perceptionsofcorruption, Happiness),            
                 list(avg = mean))  %>%  
    select(-Countryname)
``` 
Wir werden für jeden Faktor das lineare Model bilden. In nächsten Wochen werden wir das auch als ein Mutivariate Analyse machen. Aber für jetzt machen wir alles seperat nur zum üben. :) Beachte wie ich den Bestimmheitsmass ausdrücke.
``` 
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
``` 
Wir haben jetzt viele Bestimmheitsmasswerte. Wir können diese unter einen Variablen speichern. Schau mal, ob wir alle Werte gespeichert haben. Wie schafft du das?
``` 
r2 <- c(LogGDPpercapita_r2, Socialsupport_r2, Healthylifeexpectancyatbirth_r2, Freedomtomakelifechoices_r2, Generosity_r2, Perceptionsofcorruption_r2)
```
Um den Korrelationskoeffizient zu berechnen, brauchen wir die Funktion sqrt()
```
r <- sqrt(r2)
``` 
Jetzt zum Figur. Das ist wie ich mache. Probiere alles zu ändern und shau für dich selbst wie du zeichnen möchtest.
```
par(mai=c(1,3,1,1))
barplot(rev(r),las=1, names.arg = colnames(mydata)[9:4], horiz = T)
```
Warum denkst du, dass ich rev(r) benutzt habe?
