Lade den Datensatz co2.csv unten. Falls du ihn unter Downloads gespeichert hast, stelle dein Arbeitsverzeichnis als Downloads ein.
<img width="815" alt="image" src="https://github.com/tbilgin/DataScienceCourse/assets/26571015/e9ecec31-37b3-413a-a6a2-32d7ec02ff70">
Jetzt lade den Datensatz zum deinem Arbeitsverzeichnis:
```
co2 = read.csv("co2.csv", header = TRUE)
```
Durchsuche den Datensatz mit den üblichen Befehlen. Finde heraus, wie viele Spalten und Zeilen, und welchen Datentyp er hat.
Sind die Daten normal verteilt?
```
shapiro.test(co2$concentration)
ggplot(co2, aes(concentration)) + geom_density()
```
<img width="397" alt="Bildschirmfoto 2023-11-15 um 16 01 13" src="https://github.com/tbilgin/DataScienceCourse/assets/26571015/1cc92098-2524-480a-baab-8b9f7fc4ba78">
<img width="443" alt="Bildschirmfoto 2023-11-15 um 16 01 24" src="https://github.com/tbilgin/DataScienceCourse/assets/26571015/fc9cc492-e571-4f39-90e3-421202d93618">

Bilde ein lineares Model zwischen CO2 und Zeit. Dann zeichne das mit ggplot.
```
ggplot(co2, aes(time, concentration)) +
  geom_point() + 
  geom_smooth(method="lm")

lm_fit=lm(concentration ~ time, data = co2)
summary(lm_fit)
```
<img width="656" alt="Bildschirmfoto 2023-11-15 um 16 04 31" src="https://github.com/tbilgin/DataScienceCourse/assets/26571015/402abe1c-89b8-4756-a893-dc2b50308b9a">
<img width="765" alt="Bildschirmfoto 2023-11-15 um 16 04 43" src="https://github.com/tbilgin/DataScienceCourse/assets/26571015/e1ea97d8-1daa-464b-b44c-cf12683578d3">

Bisschen komisch! Schauen wir mal auf die Residuen. Erinnere dich daran, dass ein Residual der Unterschied zwischen dem Wert und dem vom Modell vorhergesagten Wert für einen gegebenen Punkt ist. Ein Regressionsmodell der kleinsten Quadrate minimiert die Summe der quadrierten Residualwerte. 
```
ggplot(co2, aes(time, residuals(lm_fit))) +
  geom_point()
```
<img width="468" alt="Bildschirmfoto 2023-11-15 um 16 11 48" src="https://github.com/tbilgin/DataScienceCourse/assets/26571015/e99be8d3-b3c5-4f42-8ea3-71f6faf560d6">

# Nicht parametrisches Modell

Wir werden jetzt ein nicht parametrisches Modell probieren. Dazu braucht man zuerst eine Formel definieren mit Werte, die das Modell schätzen wird. Unsere Formel ist y~a+b*x+c*x^2, wo a, b, und c die Werte zum Schätzen sind.
```
Werte=list(a=1,b=1,c=1) 
nl_fit=nls(concentration ~ b + a * time + c * time^2,
           data = co2,
           start = Werte)
summary(nl_fit)
ggplot(co2, aes(time, residuals(nl_fit))) +
  geom_point()
```
<img width="689" alt="Bildschirmfoto 2023-11-15 um 16 18 36" src="https://github.com/tbilgin/DataScienceCourse/assets/26571015/63ac1422-7e4c-49c6-a87c-a7574aa18d98">

<img width="468" alt="Bildschirmfoto 2023-11-15 um 16 18 58" src="https://github.com/tbilgin/DataScienceCourse/assets/26571015/d92c2218-3433-45c7-abf8-a9f541aaf4d5">

Die Residuen sehen viel besser aus, weil sie jetzt um 0 verteilt sind.
Und hier ist, wie man das Plot zeichnet.
```
ggplot(co2, aes(time, concentration)) +
  geom_point() + 
stat_smooth(method = 'nls', formula = 'y~a+b*x+c*x^2',
            method.args = list(start=Werte), se=FALSE)
```
<img width="963" alt="Bildschirmfoto 2023-11-15 um 16 21 47" src="https://github.com/tbilgin/DataScienceCourse/assets/26571015/d2c424d1-ad16-44c0-9a7b-9bac19d49f5b">

Schön aber man muss an die Schwankungen denken, und darüber was machen.

Also ein neues Modell:
```
Werte = list(a=1,b=1,c=1,d=1,e=1) 
sin_fit=nls(concentration ~ b+a*time+ c*time^2+d*sin(2*pi*time+e),
           data = co2,
           start = Werte) 
```

```
summary(sin_fit)

ggplot(co2, aes(time, residuals(sin_fit))) +
  geom_point()

ggplot(co2, aes(time, concentration)) +
  geom_point() + 
  stat_smooth(method = 'nls', formula = 'y ~ b+a*x+ c*x^2+d*sin(2*pi*x+e)',
              method.args = list(start=Werte), se=FALSE)
```
<img width="754" alt="Bildschirmfoto 2023-11-15 um 16 33 35" src="https://github.com/tbilgin/DataScienceCourse/assets/26571015/542f2c26-6bf3-4e31-8c1d-2ee112a26a9a">
<img width="370" alt="Bildschirmfoto 2023-11-15 um 16 34 10" src="https://github.com/tbilgin/DataScienceCourse/assets/26571015/b428d50c-0528-4603-84f4-6a265a7acb7d">
<img width="814" alt="Bildschirmfoto 2023-11-15 um 16 33 48" src="https://github.com/tbilgin/DataScienceCourse/assets/26571015/0d1452a7-7faa-4572-9e11-30d966eae290">

Jetzt sehen wir mal alle zusammen:
```














