# Lineare_Regression

## Dateanalyse mit Tidyverse

``
    
     mydata %>%                                           # Datenauswahl               
     group_by(Countryname) %>%                            # Gruppenauswahl
     summarise_at(vars(LogGDPpercapita, Happiness),       # Spaltenauswahl
                  list(avg = mean))                       # Funktion  
                  
``
<img width="374" alt="Bildschirmfoto 2023-09-27 um 12 18 45" src="https://github.com/tbilgin/DataScienceCourse/assets/26571015/87cc573b-9014-4bdd-b465-6eb417911cb4">

