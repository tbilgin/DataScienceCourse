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



## Mehrere Beispiele
```
mydata  %>%  filter(Countryname == "Switzerland" & Year > 2010) %>% group_by(Year)
```

  Countryname  Year Happiness LogGDPpercapita Socialsupport Healthylifeexpectancyat…¹ Freedomtomakelifecho…²
  <chr>       <int>     <dbl>           <dbl>         <dbl>                     <dbl>                  <dbl>
1 Switzerland  2012      7.78            10.9         0.947                      72.8                  0.945
2 Switzerland  2014      7.49            11.0         0.959                      73.1                  0.949
3 Switzerland  2015      7.57            11.0         0.938                      73.2                  0.928
4 Switzerland  2016      7.46            11.0         0.928                      73.5                  0.934
5 Switzerland  2017      7.47            11.0         0.950                      73.8                  0.925
6 Switzerland  2018      7.51            11.0         0.930                      74.1                  0.926

```
mydata  %>%  group_by(Countryname, Year)
```

   Countryname  Year Happiness LogGDPpercapita Socialsupport Healthylifeexpectancya…¹ Freedomtomakelifecho…²
   <chr>       <int>     <dbl>           <dbl>         <dbl>                    <dbl>                  <dbl>
 1 Afghanistan  2008      3.72            7.17         0.451                     50.8                  0.718
 2 Afghanistan  2009      4.40            7.33         0.552                     51.2                  0.679
 3 Afghanistan  2010      4.76            7.39         0.539                     51.6                  0.600
 4 Afghanistan  2011      3.83            7.42         0.521                     51.9                  0.496
 5 Afghanistan  2012      3.78            7.52         0.521                     52.2                  0.531
 6 Afghanistan  2013      3.57            7.52         0.484                     52.6                  0.578
 7 Afghanistan  2014      3.13            7.52         0.526                     52.9                  0.509
 8 Afghanistan  2015      3.98            7.50         0.529                     53.2                  0.389
 9 Afghanistan  2016      4.22            7.50         0.559                     53                    0.523
10 Afghanistan  2017      2.66            7.50         0.491                     52.8                  0.427

```
mydata %>% group_by(Countryname, Year) %>%  select(-(LogGDPpercapita:Socialsupport)) %>% 
     group_by(Countryname) %>% 
     filter(Generosity == min(Generosity))
```

   Countryname  Year Happiness Healthylifeexpectancyatbirth Freedomtomakelifechoices Generosity
   <chr>       <int>     <dbl>                        <dbl>                    <dbl>      <dbl>
 1 Afghanistan  2017      2.66                         52.8                    0.427    -0.112 
 2 Albania      2011      5.87                         66.7                    0.487    -0.208 
 3 Algeria      2011      5.32                         64.7                    0.530    -0.204 
 4 Angola       2014      3.79                         54.6                    0.375    -0.157 
 5 Argentina    2018      5.79                         68.8                    0.846    -0.207 
 6 Armenia      2007      4.88                         64.9                    0.605    -0.237 
 7 Australia    2018      7.18                         73.6                    0.916     0.138 
 8 Austria      2018      7.40                         73                      0.904     0.0516
 9 Azerbaijan   2006      4.73                         61.9                    0.772    -0.253 
10 Bahrain      2011      4.82                         66.6                    0.870    -0.0593

```
mydata %>% 
     group_by(Countryname) %>% 
     summarise(avg_GDP = mean(LogGDPpercapita), st_dev = sd(LogGDPpercapita))
```

   Countryname avg_GDP  st_dev
   <chr>         <dbl>   <dbl>
 1 Afghanistan    7.44 0.110  
 
 2 Albania        9.26 0.0960 
 
 3 Algeria        9.51 0.0418 
 
 4 Angola         8.71 0.0264 
 
 5 Argentina      9.83 0.0487 
 
 6 Armenia        8.93 0.118  
 
 7 Australia     10.7  0.0355 
 
 8 Austria       10.7  0.0218 
 
 9 Azerbaijan     9.63 0.123  
 
10 Bahrain       10.6  0.00708

