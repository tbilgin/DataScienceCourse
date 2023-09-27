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

## Dateanalyse mit Tidyverse

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


