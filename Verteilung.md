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
Obere_Grenze = mean(Verteilung) + Kon_95
Obere_Grenze
Untere Grenze = mean(Verteilung) - Kon_95
Untere Grenze
```
<img width="477" alt="Bildschirmfoto 2023-10-16 um 13 19 11" src="https://github.com/tbilgin/DataScienceCourse/assets/26571015/f6ac5a34-a458-4f74-bae2-0c959ae19eb8">


Jetzt zum Plot:
Zuerst löschen wir bisherige Plot Einstellunggen. Dann hist. 
```
dev.off()
hist(Verteilung, breaks = 5)
```

Probiere mit unterschiedlichen breaks. Funktioniert nicht gut. 
<img width="460" alt="Bildschirmfoto 2023-10-16 um 13 07 17" src="https://github.com/tbilgin/DataScienceCourse/assets/26571015/0cb85453-698e-49c1-a877-5ac0e1507b36">

Man kann dann bischen mehr spezifisch sein. 
```
hist(Verteilung, breaks=c(seq(0, 20, by= 4)))
```

<img width="473" alt="Bildschirmfoto 2023-10-16 um 13 04 45" src="https://github.com/tbilgin/DataScienceCourse/assets/26571015/fdde15a5-9b57-4843-b2c3-1d142bef0a5c">
Probiere unterschiedliche Parametern mit seq Funktion.

Jetzt fügen wir den Durchschnittslinie dazu ein.
```
abline(v=mean(Verteilung), col = "darkblue", lwd = 3)
```
<img width="454" alt="Bildschirmfoto 2023-10-16 um 13 21 36" src="https://github.com/tbilgin/DataScienceCourse/assets/26571015/13aeef0b-996e-46a3-a81b-bcc1b21aa93d">


Kennst du all alle Parameter drin? Probiere die zu ändern.

Jetzt fügen wir die Konfidenzintervalle dazu ein.
```
abline(v=Obere_Grenze, col = "darkblue")
abline(v=Untere_Grenze, col = "darkblue")
```

<img width="439" alt="Bildschirmfoto 2023-10-16 um 13 20 41" src="https://github.com/tbilgin/DataScienceCourse/assets/26571015/b80cd629-fce0-4ace-9026-e5c3a1efda46">











