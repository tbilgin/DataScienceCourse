Wir werden die gängigste Masszahlen für die Verspätungsverteilung berechnen.
Zuerst erstellen wir die Variabel.

```
Verteilung = c(1,1, 2, rep(5, 6), rep(10,6), 20)
max(Verteilung)
min(Verteilung)
mean(Verteilung)
summary(Verteilung)
sd(Verteilung)
```
<img width="197" alt="Bildschirmfoto 2023-10-16 um 12 12 25" src="https://github.com/tbilgin/DataScienceCourse/assets/26571015/dda7426b-4602-42aa-9393-a35bab39fe74">
<img width="539" alt="Bildschirmfoto 2023-10-16 um 12 13 08" src="https://github.com/tbilgin/DataScienceCourse/assets/26571015/1f9db83b-3bd9-4e5d-ab24-63b6a86b98f8">

Nächtes berechnen wir die Konfidenzintervalle:
```
Kon_95 = 1.96 * sd(Verteilung) / sqrt(length(Verteilung))
Kon_95
Obere_Grenze = mean(Verteilung) - Kon_95
Obere_Grenze
Untere Grenze = mean(Verteilung) + Kon_95
Untere Grenze
```
<img width="654" alt="Bildschirmfoto 2023-10-16 um 12 14 50" src="https://github.com/tbilgin/DataScienceCourse/assets/26571015/ac733e58-b14c-4637-9e49-db34ff9457fe">






