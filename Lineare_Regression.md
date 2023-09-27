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

Und wir können auch alles über die Regression mit dem Befehl überfahren:
```
summary(trend)
```
<img width="505" alt="Bildschirmfoto 2023-09-27 um 15 19 17" src="https://github.com/tbilgin/DataScienceCourse/assets/26571015/c668b80a-827e-452d-8036-3d623181bfa5">

Hier ist -1.2678 der y-Achenabscnitt und 0.7254 ist die Steigung.
Bestimmheitsmass ist sagt uns wie gut die lienare Regression die Variation unserer Beobachtung erklärt. Es ist das Quadrat der Korrelation. Also dann wie berechnet man die Korrelation zwischen dem Einkommen und der Glücklichkeit einer Nation?





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
trend<-lm(Happiness_avg ~ <Faktor>_avg, data = Einkommen)
abline(trend,col="<deine ausgewählte Farbe>")
summary(trend)
# berechne die Wurzel des Bestimmheitsmasses
```

