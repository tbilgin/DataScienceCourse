# Lineare_Regression

## Dateanalyse mit Tidyverse

``
    
     mydata %>%                                           # Datenauswahl               

     group_by(Countryname) %>%                            # Gruppenauswahl
      
     summarise_at(vars(LogGDPpercapita, Happiness),       # Spaltenauswahl 
     
                  list(avg = mean))                       # Funktion  
                  
``

